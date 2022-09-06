<template>
<CardUser :user-info="user" />
</template>

<script setup lang="ts">
    definePageMeta({
        layout: "dashboard",
    });
    const route = useRoute();

    const user_id = route.params.userID as string;

    const user = ref({
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
        });

            const res = await fetch(`https://api.policepublic.in/u/${user_id}/get`, {
        headers: { Authorization: localStorage.getItem("ppc_token") },
    });

        if (res.status == 200) {
        const {users: cInfo} = await res.json();
        console.log(cInfo);
        user.value = cInfo.map((x) => {
            x.user_dob = new Date(x.user_dob);
            return x;
        });
    }
</script>
