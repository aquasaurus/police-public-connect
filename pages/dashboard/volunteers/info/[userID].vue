<template>
    <div class="p-2 w-full">
        <div class="bg-black/20 w-full shadow-lg">
            <div
                :class="`transition-all duration-500 ease-in-out overflow-y-hidden px-4 w-full`"
            >
                <div class="grid grid-cols-1 mx-auto gap-8 items-start">
                    <div class="p-2 flex flex-col space-y-4 items-center text-center mx-auto">
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Person Name</span
                            >
                            <span class="text-base">{{
                                user.user_name
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Volunteer ID</span
                            >
                            <span class="text-base">{{
                                user.user_id
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Contact Number</span
                            >
                            <span class="text-base">{{
                                user.user_phone
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Email ID</span
                            >
                            <span class="text-base">{{
                                user.user_email
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Date of Birth</span
                            >
                            <span class="text-base">{{
                                user.user_dob
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Address</span
                            >
                            <span class="text-base">{{
                                user.user_address
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >City</span
                            >
                            <span class="text-base">{{
                                user.user_city
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Pincode</span
                            >
                            <span class="text-base">{{
                                user.user_pincode
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Aadhar Number</span
                            >
                            <span class="text-base">{{
                                user.user_aadhar
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Father Name</span
                            >
                            <span class="text-base">{{
                                user.user_father_name
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Mother Name</span
                            >
                            <span class="text-base">{{
                                user.user_mother_name
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Parent Mobile Number</span
                            >
                            <span class="text-base">{{
                                user.user_parent_phone
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Previous experience</span
                            >
                            <span class="text-base">{{
                                user.user_experience_desc
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Health issues</span
                            >
                            <span class="text-base">{{
                                user.user_health_desc
                            }}</span>
                        </div>
                        
                        <!--
                            <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >FIELD NAME</span
                            >
                            <span class="text-base">{{
                                user.field_name
                            }}</span>
                        </div>
                        -->
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Account Type</span
                            >
                            <span class="text-base">{{
                                user.user_level === 1
                                    ? "Unverified"
                                    : user.user_level === 2
                                    ? "Volunteer"
                                    : user.user_level === 3
                                    ? "Dummy"
                                    : user.user_level === 4
                                    ? "Admin"
                                    : "Unknown"
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Do you have previous experience?</span
                            >
                            <span class="text-base">{{
                                user.user_experience
                                    ? user.user_experience_description
                                    : "None"
                            }}</span>
                        </div>
                    </div>
                    <div class="p-2 flex flex-col items-center">
                        <button
                            v-if="user.user_level === 1"
                            class="p-2 text-center bg-blue-400 text-white rounded-xl transition duration-500 ease-in-out transform hover:-translate-y-1"
                            @click="approveUser"
                        >
                            Approve User
                        </button>
                        <button
                            v-else-if="user.user_level === 2"
                            class="p-2 text-center bg-blue-400 text-white rounded-xl transition duration-500 ease-in-out transform hover:-translate-y-1"
                            @click="deactivateUser"
                        >
                            Deactivate User
                        </button>
                    </div>
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
        })[0];
    }

    async function approveUser() {
        const res = await fetch(`https://api.policepublic.in/u/${user.user_id}/verify`, {
            method: "GET",
            headers: { Authorization: localStorage.getItem("ppc_token") },
        });
        if (res.status == 200) {
            history.go(0);
        }
    }

    async function deactivateUser() {
        const res = await fetch(`https://api.policepublic.in/u/${user.user_id}/unverify`, {
            method: "GET",
            headers: { Authorization: localStorage.getItem("ppc_token") },
        });
        if (res.status == 200) {
            history.go(0);
        }
    }
</script>
