<template>
    <span>Logging you out</span>
</template>

<script setup lang="ts">
    localStorage.removeItem("ppc_token");
    navigateTo("/");
</script>
