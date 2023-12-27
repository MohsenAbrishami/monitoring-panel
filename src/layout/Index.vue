<template>
    <div>
        <app-header />
        <slot />
        <app-footer />
    </div>
</template>

<script setup>
import AppHeader from './Header.vue'
import AppFooter from './Footer.vue'
</script>
