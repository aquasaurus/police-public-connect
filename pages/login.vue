<template>
    <form
        ref="loginForm"
        class="max-w-xl w-full mx-auto py-12 p-2 flex flex-col space-y-4"
        @submit="validateForm"
    >
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
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
                class="p-2 rounded-xl max-w-md w-full border-zinc-400 focus:border-blue-400 border"
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
                class="required p-2 rounded-xl max-w-md w-full border-zinc-400 focus:border-blue-400 border"
                required
            />
        </div>
        <MiscMessage :class = "message.content ? `visible` : `invisible`" :type="message.type">{{ message.content }}</MiscMessage>
        <a href = "/apply" class = "decoration-transparent text-blue-400">Not a volunteer yet? Apply!</a>
        <button
            type="submit"
            class="max-w-md mx-auto text-white rounded-xl p-4 w-full bg-blue-400 transition duration-500 ease-in-out transform hover:-translate-y-1"
        >
            Login / உள்நுழை
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
        };
        if (Array.from(formData.values()).some((x) => !x))
            return anErrorOccured(
                "Please check whether all data has been entered properly."
            );
        const auth = await fetch("https://api.policepublic.in/auth", {method: "POST", body: JSON.stringify({user_email: accountInfo.user_email, user_password: accountInfo.user_password})})
        if(auth.status===200) {
            const {token} = await auth.json()
            localStorage.setItem("ppc_token", token);
            window.location.href="/dashboard"
        }
        else return anErrorOccured("Invalid credentials.")
    }
    function anErrorOccured(msg: string) {
        message.value.content = msg;
        message.value.type = "error";
    }
</script>
