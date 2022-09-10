<template>
    <div class="p-2 w-full">
        <div class="bg-black/20 w-full shadow-lg">
            <div
                class="flex flex-row items-center rounded-t-xl border-b-2 border-blue-400 px-4 py-6 justify-between cursor-pointer"
                @click="() => (userOpen = !userOpen)"
            >
                <span>{{ userInfo.user_name }} #{{ userInfo.user_id }}</span>
                <button
                    :class="`stroke-2 stroke-white transition duration-500 ease-in-out transform ${
                        userOpen ? `rotate-180` : `rotate-0`
                    }`"
                    @click="() => (userOpen = !userOpen)"
                >
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        width="24"
                        height="24"
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        class="feather feather-chevron-down"
                    >
                        <polyline points="6 9 12 15 18 9"></polyline>
                    </svg>
                </button>
            </div>
            <div
                :class="`transition-all duration-500 ease-in-out overflow-y-hidden px-4 ${
                    userOpen ? `max-h-[70rem] py-4` : `max-h-0`
                } w-full`"
            >
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-start">
                    <div class="p-2 flex flex-col space-y-4">
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Person Name</span
                            >
                            <span class="text-base">{{
                                userInfo.user_name
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Contact Number</span
                            >
                            <span class="text-base">{{
                                userInfo.user_phone
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Email ID</span
                            >
                            <span class="text-base">{{
                                userInfo.user_email
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Date of Birth</span
                            >
                            <span class="text-base">{{
                                userInfo.user_dob
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Address</span
                            >
                            <span class="text-base">{{
                                userInfo.user_address
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >City</span
                            >
                            <span class="text-base">{{
                                userInfo.user_city
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Pincode</span
                            >
                            <span class="text-base">{{
                                userInfo.user_pincode
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Aadhar Number</span
                            >
                            <span class="text-base">{{
                                userInfo.user_aadhar
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Father Name</span
                            >
                            <span class="text-base">{{
                                userInfo.user_father_name
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Mother Name</span
                            >
                            <span class="text-base">{{
                                userInfo.user_mother_name
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Parent Mobile Number</span
                            >
                            <span class="text-base">{{
                                userInfo.user_parent_phone
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Previous experience</span
                            >
                            <span class="text-base">{{
                                userInfo.user_experience_desc
                            }}</span>
                        </div>
                        <div class="flex flex-col space-y-1 break-words">
                            <span class="font-semibold text-lg uppercase"
                                >Health issues</span
                            >
                            <span class="text-base">{{
                                userInfo.user_health_desc
                            }}</span>
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
                    <div class="p-2 flex flex-col items-center space-y-4">
                        <button
                            v-if="userInfo.user_level === 1"
                            class="p-2 text-center bg-blue-400 text-white rounded-xl transition duration-500 ease-in-out transform hover:-translate-y-1"
                            @click="approveUser"
                        >
                            Approve User
                        </button>
                        <button
                            v-else-if="userInfo.user_level === 2"
                            class="p-2 text-center bg-blue-400 text-white rounded-xl transition duration-500 ease-in-out transform hover:-translate-y-1"
                            @click="deactivateUser"
                        >
                            Deactivate User
                        </button>
                        <a
                            :href = "`/dashboard/volunteers/data/${userInfo.user_id}`"
                            class="p-2 text-center bg-blue-400 text-white rounded-xl transition duration-500 ease-in-out transform hover:-translate-y-1"
                        >
                            Printable
                    </a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
    const userOpen = ref(false);

    const { userInfo } = defineProps({ userInfo: Object });

    async function approveUser() {
        const res = await fetch(`https://api.policepublic.in/u/${userInfo.user_id}/verify`, {
            method: "GET",
            headers: { Authorization: localStorage.getItem("ppc_token") },
        });
        if (res.status == 200) {
            history.go(0);
        }
    }

    async function deactivateUser() {
        const res = await fetch(`https://api.policepublic.in/u/${userInfo.user_id}/unverify`, {
            method: "GET",
            headers: { Authorization: localStorage.getItem("ppc_token") },
        });
        if (res.status == 200) {
            history.go(0);
        }
    }
</script>
