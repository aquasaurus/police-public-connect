<template>
    <form
        ref="loginForm"
        class="max-w-xl w-full mx-auto py-12 p-2 flex flex-col space-y-4"
        @submit="validateForm"
    >
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
            <label
                for="user_name"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Name</label
            >
            <input
                type="text"
                name="Name"
                id="user_name"
                placeholder="பெயர்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_email"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Email ID</label
            >
            <input
                type="email"
                name="user_email"
                id="user_email"
                placeholder="மின்னஞ்சல்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_phone"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Phone Number</label
            >
            <input
                type="text"
                name="Phone"
                id="user_phone"
                placeholder="தொலைபேசி எண்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_date_of_birth"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Date of Birth</label
            >
            <input
                type="Date"
                name="DOB"
                id="user_date_of_birth"
                placeholder="பிறந்த தேதி"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="Gender"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Gender</label
            >
            {{ gender }}
            <select 
                v-model="gender"
                type="text"
                name="user_sex"
                id="Gender"
                placeholder="பாலினம்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            >
                <option value="Male">Male</option>
                <option value="Female">Female</option>
                <option value="Other">Other</option>
                <option value="Not to say">Not to say</option>
            </select>
            <label
                for="user_address"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Address</label
            >
            <input
                type="text"
                name="Address"
                id="user_address"
                placeholder="முகவரி"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_city"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >City</label
            >
            <input
                type="text"
                name="City"
                id="user_city"
                placeholder="நகரம்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_pincode"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Pincode</label
            >
            <input
                type="text"
                name="Pincode"
                id="user_pincode"
                placeholder="அஞ்சல் குறியீடு"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_aadhar"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Aadhar Number</label
            >
            <input
                type="text"
                name="Aadhar"
                id="user_aadhar"
                placeholder="ஆதார் எண்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_password"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                >Password</label
            >
            <input
                type="password"
                name="user_password"
                id="user_password"
                placeholder="கடவுச்சொல்"
                class="required p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
        </div>
        <MiscMessage :class = "message.content ? `visible` : `invisible`" :type="message.type">{{ message.content }}</MiscMessage>
        <a href = "/login" class = "decoration-transparent text-blue-400">Already have an account? Sign in!</a>
        <button
            type="submit"
            class="max-w-md mx-auto text-white rounded-xl p-4 w-full bg-blue-400 transition duration-500 ease-in-out transform hover:-translate-y-1"
        >
            Apply / விண்ணப்பிக்க
        </button>
    </form>
</template>

<script setup lang="ts">
    const loginForm = ref<HTMLFormElement>(null);
    const message = ref<{ type: string; content: string }>({
        type: "",
        content: "",
    });

    function validateForm(e: SubmitEvent) {
        e.preventDefault();
        const formData = new FormData(loginForm.value);
        const accountInfo = {
            user_email: formData.get("user_email"),
            user_password: formData.get("user_password"),
        };
        if (Array.from(formData.values()).some((x) => !x))
            return anErrorOccured(
                "Please check whether all data has been entered properly."
            );
    }
    function anErrorOccured(msg: string) {
        message.value.content = msg;
        message.value.type = "error";
    }
</script>
