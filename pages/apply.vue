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
                name="user_name"
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
                name="user_phone"
                id="user_phone"
                pattern="^(?:\+91)?[0-9]{10}$"
                title="Phone number should be a ten-digit number"
                placeholder="தொலைபேசி எண்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_dob"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Date of Birth</label
            >
            <input
                type="Date"
                name="user_dob"
                id="user_dob"
                placeholder="பிறந்த தேதி"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Blood Group</label
            >
            <input
                type="text"
                name="user_bloodgroup"
                id="user_bloodgroup"
                placeholder="இரத்த வகை"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_address"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Address</label
            >
            <input
                type="text"
                name="user_address"
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
                name="user_city"
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
                name="user_pincode"
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
                name="user_aadhar"
                id="user_aadhar"
                placeholder="ஆதார் எண்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_father_name"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Father Name</label
            >
            <input
                type="text"
                name="user_father_name"
                id="user_father_name"
                placeholder="தந்தையின் பெயர்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_mother_name"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Mother Name</label
            >
            <input
                type="text"
                name="user_mother_name"
                id="user_mother_name"
                placeholder="தாய் பெயர்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_parent_phone"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Parent Phone Number</label
            >
            <input
                type="text"
                name="user_parent_phone"
                id="user_parent_phone"
                placeholder="பெற்றோர் தொலைபேசி எண்"
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
            <label
                for="confirm_password"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                >Confirm Password</label
            >
            <input
                type="password"
                name="confirm_password"
                id="confirm_password"
                placeholder="கடவுச்சொல்"
                class="required p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_health"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                >Any Health issues</label
            >
            <input
                type="checkbox"
                name="user_health"
                id="user_health"
                placeholder=""
                class="required p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                
            />
            <label
                for="user_health_desc"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                >If Yes, Mention it</label
            >
            <input
                type="text"
                name="user_health_desc"
                id="user_health_desc"
                placeholder="Leave empty if none"
                class="required p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
            />
            <label
                for="user_experience"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                >Any Past Volunteering Experience</label
            >
            <input
                type="checkbox"
                name="user_experience"
                id="user_experience"
                placeholder=""
                class="required p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
    
            />
            <label
                for="user_experience_desc"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                >If Yes, Mention it</label
            >
            <input
                type="text"
                name="user_experience_desc"
                id="user_experience_desc"
                placeholder="Leave empty if none"
                class="required p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
            />
            
        </div>
        <label
                for="user_agree_to_terms"
                class="font-semibold text-base text-red-600 uppercase text-center lg:text-left w-full"
                >I hereby declare that information provided by me is correct to my fullest knowledge</label
            >
            <input
                type="checkbox"
                name="user_dummy"
                id="user_agree_to_terms"
                placeholder=""
                class="required p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="user_agree_to_terms"
                class="font-semibold text-base text-red-600 uppercase text-center lg:text-left w-full"
                >I further agree and submit this form with the consent of my parents or guardian to carry out this social activity for the benefit of public.</label
            >
            <input
                type="checkbox"
                name="user_agree_to_terms"
                id="user_agree_to_terms"
                placeholder=""
                class="required p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
        <MiscMessage
            :class="message.content ? `visible` : `invisible`"
            :type="message.type"
            >{{ message.content }}</MiscMessage
        >
        <a href="/login" class="decoration-transparent text-blue-400"
            >Already have an account? Sign in!</a
        >
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

    async function validateForm(e: SubmitEvent) {
        e.preventDefault();
        const formData = new FormData(loginForm.value);
        const accountInfo = {
            user_email: formData.get("user_email"),
            user_password: formData.get("user_password"),
            user_name: formData.get("user_name"),
            user_phone: formData.get("user_phone"),
            user_dob: formData.get("user_dob"),
            user_sex: formData.get("user_sex"),
            user_address: formData.get("user_address"),
            user_city: formData.get("user_city"),
            user_pincode: formData.get("user_pincode"),
            user_aadhar: formData.get("user_aadhar"), 
            user_experience: formData.get("user_experience"),//*
            user_experience_desc: formData.get("user_experience_desc"), //*
            user_agree_to_terms: formData.get("user_agree_to_terms"), //*
            user_health: formData.get("user_health"),//*
            user_health_desc: formData.get("user_health_desc"),//*
            user_father_name: formData.get("user_father_name"),
            user_mother_name: formData.get("user_mother_name"),
            user_parent_phone: formData.get("user_parent_phone"),
        };
        if(accountInfo.user_password !== formData.get("confirm_password")) {
            return anErrorOccured("Passwords don't match");
        }
        if((accountInfo.user_aadhar as string).length !== 12) {
            return anErrorOccured("Invalid aadhar number");
        }
        if((accountInfo.user_phone as string).length !== 10) {
            return anErrorOccured("Invalid mobile number");
        }
        if(accountInfo.user_experience && !accountInfo.user_experience_desc) {
            return anErrorOccured("Please describe your previous experience.");
        }
        if(accountInfo.user_health && !accountInfo.user_health_desc) {
            return anErrorOccured("Please describe your health issues.");
        }

/*        if (Array.from(formData.values()).some((x) => !x))
            return anErrorOccured(
                "Please check whether all data has been entered properly."
            );*/
        const auth = await fetch("https://api.policepublic.in/users/new", {
            method: "POST",
            body: JSON.stringify(accountInfo),
        });
        if (auth.status === 200) {
            message.value.content = "Application Successfull. Check your email for a confirmation link.";
            message.value.type = "success";
            loginForm.value.reset()
        } else return anErrorOccured("Invalid credentials.");
    }
    function anErrorOccured(msg: string) {
        message.value.content = msg;
        message.value.type = "error";
    }
</script>
