<template>
  <div>
    <Suspense>
      <template #default>
        <AsyncCityView />
      </template>
      <template #fallback>
        <p> loding</p>
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import AsyncCityView from "../components/AsyncCityView.vue";
</script>