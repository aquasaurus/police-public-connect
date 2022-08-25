<template>
    <div class="max-w-6xl mx-auto flex flex-col space-y-4">
        <CardUser
            v-for="user in users"
            :key="`user_${user.user_id}`"
            :user-info="user"
        />
    </div>
</template>
<script setup>
    definePageMeta({
        layout: "dashboard",
    });

    const users = [
        {
            user_name: "Deva",
            user_email: "devadummy@gmail.com",
            user_password: "devapassword",
            user_phone: "1234554321",
            user_date_of_birth: new Date("1996-04-09"),
            user_sex: "F",
            user_id: "V124",
            user_address: "Adani street",
            user_city: "chennai",
            user_pincode: "600000",
            user_aadhar: "1234 4567 1234",
        },
        {
            user_name: "Ajal",
            user_email: "ajaldummy@gmail.com",
            user_password: "ajalgondhara",
            user_phone: "8879685678",
            user_date_of_birth: new Date("2002-08-24"),
            user_sex: "M",
            user_id: "V234",
            user_address: "Mridhulan Street",
            user_city: "chennai",
            user_pincode: "600003",
            user_aadhar: "6734 4567 1234",
        },
        {
            user_name: "Srithula",
            user_email: "srithuladoesnotexist@gmail.com",
            user_password: "srithulasrithula",
            user_phone: "7865745673",
            user_date_of_birth: new Date("2000-12-09"),
            user_sex: "F",
            user_id: "V023",
            user_address: "Swaptha Street",
            user_city: "chennai",
            user_pincode: "600023",
            user_aadhar: "7777 4567 1234",
        },
    ];
</script>
