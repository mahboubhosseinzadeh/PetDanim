<template>
    <div>
        <Header />
        <slot />
    </div>

</template>

<script setup>
import Header from "@/components/Header/Header.vue";
definePageMeta({
    colorMode: "light",
});
</script>
