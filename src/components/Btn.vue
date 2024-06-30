<template>
  <div>
    <Button
        :severity="btnProps.severity"
        :icon="btnProps.icon"
        :raised="btnProps.raised"
        :rounded="btnProps.rounded"
    />
  </div>
</template>

<script setup>
import {ref, defineProps} from 'vue'
import Button from 'primevue/button';
const btnProps = defineProps(['severity', 'icon', 'raised', 'rounded'])

</script>

<style scoped>

</style>