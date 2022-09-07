<template>
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-start">
        <div class="p-2 flex flex-col space-y-4">
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase">Person Name</span>
                <span class="text-base">{{ userInfo.user_name }}</span>
            </div>
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase"
                    >Contact Number</span
                >
                <span class="text-base">{{ userInfo.user_phone }}</span>
            </div>
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase">Email ID</span>
                <span class="text-base">{{ userInfo.user_email }}</span>
            </div>
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase"
                    >Date of Birth</span
                >
                <span class="text-base">{{ userInfo.user_dob }}</span>
            </div>
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase">Address</span>
                <span class="text-base">{{ userInfo.user_address }}</span>
            </div>
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase">City</span>
                <span class="text-base">{{ userInfo.user_city }}</span>
            </div>
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase">Pincode</span>
                <span class="text-base">{{ userInfo.user_pincode }}</span>
            </div>
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase"
                    >Aadhar Number</span
                >
                <span class="text-base">{{ userInfo.user_aadhar }}</span>
            </div>
            <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase">Father Name</span>
                    <span class="text-base">{{ userInfo.user_father_name }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase">Mother Name</span>
                    <span class="text-base">{{ userInfo.user_mother_name }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase">Parent Mobile Number</span>
                    <span class="text-base">{{ userInfo.user_parent_phone }}</span>
                </div>
                <div class="flex flex-col space-y-1 break-words items-center">
                    <span class="font-semibold text-lg uppercase">Health Issues</span>
                    <span class="text-base">{{ userInfo.user_health_desc || "None" }}</span>
                </div>
            <!--
                            <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >FIELD NAME</span
                            >
                            <span class="text-base">{{
                                userInfo.field_name
                            }}</span>
                        </div>
                        -->
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase"
                    >Account Type</span
                >
                <span class="text-base">{{
                    userInfo.user_level === 1
                        ? "Unverified"
                        : userInfo.user_level === 2
                        ? "Volunteer"
                        : userInfo.user_level === 3
                        ? "Dummy"
                        : userInfo.user_level === 4
                        ? "Admin"
                        : "Unknown"
                }}</span>
            </div>
            <div class="flex flex-col space-y-1 break-words">
                <span class="font-semibold text-lg uppercase"
                    >Do you have previous experience?</span
                >
                <span class="text-base">{{
                    userInfo.user_experience
                        ? userInfo.user_experience_description
                        : "None"
                }}</span>
            </div>
        </div>
    </div>
</template>


<script setup lang="ts">
    definePageMeta({
        layout: "plain"
    })
    const route = useRoute();

    const user_id = route.params.userID as string;

    const userInfo = ref<Record<string, unknown>>({
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
        const { users: cInfo } = await res.json();
        console.log(cInfo);
        userInfo.value = cInfo.map((x) => {
            x.user_dob = new Date(x.user_dob);
            return x;
        })[0];
    }
</script>
