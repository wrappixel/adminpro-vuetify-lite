<script setup lang="ts">
import { RouterLink } from "vue-router";
</script>
<template>
    <div class="logo">
      <RouterLink to="/" class="d-flex">
        <img src="@/assets/images/logos/dark-logo-icon.svg" />
        <img src="@/assets/images/logos/dark-logo-text.svg" class="pl-3" />
      </RouterLink>
    </div>
  </template>
