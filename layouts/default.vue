<template>
  <navbar v-if="$route.name !== 'index'" :key="$route.fullpath"/>
  <slot />
</template>

<script lang="ts">
export default defineComponent({

})
</script>

<style scoped>

</style>