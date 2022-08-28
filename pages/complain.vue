<template>
    <form
        ref="complaintForm"
        class="max-w-xl w-full mx-auto py-12 p-2 flex flex-col space-y-4"
        @submit="validateForm"
    >
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
            <label
                for="complaint_name"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                required
                >Name</label
            >
            <input
                type="text"
                name="complaint_name"
                id="complaint_name"
                placeholder="உங்கள் பெயர்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="complaint_phone"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                >Your contact number</label
            >
            <input
                type="text"
                name="complaint_phone"
                id="complaint_phone"
                pattern="^(?:\+91)?[0-9]{10}$"
                title="Phone number should be a ten-digit number"
                placeholder="உங்கள் மொபைல் எண்"
                class="required p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
            <label
                for="complaint_content"
                class="font-semibold text-base uppercase text-center lg:text-left w-full"
                >Describe your complaint</label
            >
            <textarea
                id="complaint_content"
                name="complaint_content"
                placeholder="உங்கள் புகாரை விவரிக்கவும்"
                class="p-2 rounded-xl max-w-md w-full border-gray-400 focus:border-blue-400 border"
                required
            />
        </div>
        <MiscMessage
            :class="message.content ? `visible` : `invisible`"
            :type="message.type"
            >{{ message.content }}</MiscMessage
        >
        <button
            type="submit"
            class="max-w-md mx-auto text-white rounded-xl p-4 w-full bg-blue-400 transition duration-500 ease-in-out transform hover:-translate-y-1"
        >
            Submit / பதிவிக்கவும்
        </button>
    </form>
</template>

<script setup lang="ts">
    const complaintForm = ref<HTMLFormElement>(null);
    const message = ref<{ type: string; content: string }>({
        type: "",
        content: "",
    });

    async function validateForm(e: SubmitEvent) {
        e.preventDefault();
        const formData = new FormData(complaintForm.value);
        const complaintInfo = {
            complaint_content: formData.get("complaint_content"),
            complaint_name: formData.get("complaint_name"),
            complaint_phone: formData.get("complaint_phone"),
        };
        if (Array.from(formData.values()).some((x) => !x))
            return anErrorOccured(
                "Please check whether all data has been entered properly."
            );
        const auth = await fetch("http://localhost:8000/complaints/new", {
            method: "POST",
            body: JSON.stringify(complaintInfo),
        });
        if (auth.status === 200) {
            message.value.content = "Complaint Successful";
            message.value.type = "success";
        } else return anErrorOccured("Invalid credentials.");
    }
    function anErrorOccured(msg: string) {
        message.value.content = msg;
        message.value.type = "error";
    }
</script>
