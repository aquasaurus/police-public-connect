<template>
    <div class="mt-12 lg:max-w-8xl mx-auto p-4">
        <div class = "text-center mx-auto text-3xl uppercase pt-8 pb-12 font-bold">User Profile</div>
        <div class="grid grid-flow-row lg:grid-cols-3 grid-cols-1 items-center my-auto gap-4 mx-auto">
                <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                    <span class="font-semibold text-lg text-amber-300 uppercase">Name</span>
                    <span class="text-base">{{ userInfo.user_name }}</span>
                </section>
                <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                    <span class="font-semibold text-amber-300 text-lg uppercase"
                        >Contact Number</span
                    >
                    <span class="text-base">{{ userInfo.user_phone }}</span>
                </section>
                <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                    <span class="font-semibold text-amber-300 text-lg uppercase"
                        >Email ID</span
                    >
                    <span class="text-base">{{ userInfo.user_email }}</span>
                </section>
                <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                    <span class="font-semibold text-amber-300 text-lg uppercase"
                        >Date of Birth</span
                    >
                    <span class="text-base">{{ userInfo.user_dob.toISOString().split("T")[0].split("-").reverse().join("-") }}</span>
                </section>
            <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                <span class="font-semibold text-amber-300 text-lg uppercase">Father Name</span>
                <span class="text-base">{{ userInfo.user_father_name }}</span>
            </section>
            <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                <span class="font-semibold text-amber-300 text-lg uppercase">Mother Name</span>
                <span class="text-base">{{ userInfo.user_mother_name }}</span>
            </section>
            <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                <span class="font-semibold text-amber-300 text-lg uppercase">Parent Mobile Number</span>
                <span class="text-base">{{ userInfo.user_parent_phone }}</span>
            </section>
            <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                <span class="font-semibold text-amber-300 text-lg uppercase">Previous Experience</span>
                <span class="text-base">{{ userInfo.user_experience_desc || "None" }}</span>
            </section>
            <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                <span class="font-semibold text-amber-300 text-lg uppercase">Health Issues</span>
                <span class="text-base">{{ userInfo.user_health_desc || "None" }}</span>
            </section>
                <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                    <span class="font-semibold text-amber-300 text-lg uppercase">Address</span>
                    <span class="text-base">{{ userInfo.user_address }}</span>
                </section>
                <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                    <span class="font-semibold text-amber-300 text-lg uppercase">City</span>
                    <span class="text-base">{{ userInfo.user_city }}</span>
                </section>
                <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                    <span class="font-semibold text-amber-300 text-lg uppercase">Pincode</span>
                    <span class="text-base">{{ userInfo.user_pincode }}</span>
                </section>
                <section class="flex flex-col space-y-1 break-words items-center justify-center bg-black/40 shadow-lg px-8 py-12 rounded-xl h-48">
                    <span class="font-semibold  text-amber-300 text-lg uppercase">Aadhar Number</span>
                    <span class="text-base">{{ userInfo.user_aadhar }}</span>
                </section>
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

    const res = await fetch(`https://api.policepublic.in/users/me`, {
        headers: { Authorization: localStorage.getItem("ppc_token") },
    });

    if (res.status == 200) {
        const { users: cInfo } = await res.json();
        userInfo.value = cInfo;
        userInfo.value.user_dob = new Date(userInfo.value.user_dob);
    }
</script>
