<template>
    <div class="mt-12">
        <div class="grid grid-cols-1 gap-8 items-start">
            <div class="p-2 flex flex-col space-y-4 mx-auto items-center">
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase">Name</span>
                    <span class="text-base">{{ userInfo.user_name }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase"
                        >Contact Number</span
                    >
                    <span class="text-base">{{ userInfo.user_phone }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase"
                        >Email ID</span
                    >
                    <span class="text-base">{{ userInfo.user_email }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase"
                        >Date of Birth</span
                    >
                    <span class="text-base">{{ userInfo.user_dob.toISOString().split("T")[0].split("-").reverse().join("-") }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase">Address</span>
                    <span class="text-base">{{ userInfo.user_address }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase">City</span>
                    <span class="text-base">{{ userInfo.user_city }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase">Pincode</span>
                    <span class="text-base">{{ userInfo.user_pincode }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase"
                        >Aadhar Number</span
                    >
                    <span class="text-base">{{ userInfo.user_aadhar }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
    definePageMeta({
        layout: "dashboard",
    });
    const route = useRoute();

    const user_id = route.params.userID as string;

    const userInfo = ref({
        user_name: "Unknown",
        user_email: "Unknown@gmail.com",
        user_phone: "Unknown",
        user_dob: new Date("1996-04-09"),
        user_sex: "F",
        user_id: "Unknown",
        user_address: "Unknown",
        user_city: "Unknown",
        user_pincode: "600000",
        user_aadhar: "Unknown",
    });

    const res = await fetch(`http://localhost:8000/users/me`, {
        headers: { Authorization: localStorage.getItem("ppc_token") },
    });

    if (res.status == 200) {
        const { users: cInfo } = await res.json();
        console.log(cInfo);
        userInfo.value = cInfo;
        userInfo.value.user_dob = new Date(userInfo.value.user_dob);
    }
</script>
