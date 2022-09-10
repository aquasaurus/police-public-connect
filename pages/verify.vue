<template>
<MiscMessage
            :class="message.content ? `visible` : `invisible`"
            :type="message.type"
            >{{ message.content }}</MiscMessage
        >
</template>

<script setup>
    const route = useRoute();
    const message = ref({
        type: "",
        content: "",
    });


    const token = route.query.token;
    if(!token) navigateTo("/")

    const res = await fetch(`https://api.policepublic.in/verify`, {
        method: "POST",
        body: `{"token": "${token}"}`
    });
    if(res.status === 200) {
        success("Email verified.")
    }
    else anErrorOccured("Token invalid or expired. Please sign up again.");
    function anErrorOccured(msg) {
        message.value.content = msg;
        message.value.type = "error";
    }
    function success(msg) {
        message.value.content = msg;
        message.value.type = "success";
    }
</script>