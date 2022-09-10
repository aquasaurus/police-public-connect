<template>
    <div class="max-w-6xl mx-auto flex flex-col space-y-4">
        <div class = "py-2">
            <input v-model = "toFilter" type = "text" placeholder="Filter by name / ID / mobile number" class = "rounded-xl h-12 p-2 w-full bg-black/20 text-white" />
        </div>
        <CardUser
            v-for="user in userInfo.filter(x => Number(toFilter) ? (x.user_id.includes(toFilter) || x.user_phone.includes(toFilter)) : x.user_name.toLowerCase().includes(toFilter.toLowerCase()))"
            :key="`user_${user.user_id}`"
            :user-info="user"
        />
    </div>
</template>
<script setup>
    definePageMeta({
        layout: "dashboard",
    });
    const toFilter = ref("")
    const userInfo = ref([]);
    const res = await fetch(`https://api.policepublic.in/users/verified`, {
        headers: { Authorization: localStorage.getItem("ppc_token") },
    });
    if (res.status == 200) {
        const {users: cInfo} = await res.json();
        userInfo.value = cInfo.map((x) => {
            x.user_dob = new Date(x.user_dob);
            return x;
        });
    } else if (res.status == 404) {
        userInfo.value = {
            user_name: "Unknown",
            user_email: "Unknown@gmail.com",
            user_password: "Unknown",
            user_phone: "Unknown",
            user_dob: new Date("1996-04-09"),
            user_sex: "F",
            user_id: "Unknown",
            user_address: "Unknown",
            user_city: "Unknown",
            user_pincode: "600000",
            user_aadhar: "Unknown",
        };
    }
</script>
