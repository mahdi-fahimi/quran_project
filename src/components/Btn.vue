<template>
  <div>
    <Button
        :severity="plusBtnProps.severity"
        :icon="plusBtnProps.icon"
        :raised="plusBtnProps.raised"
        :rounded="plusBtnProps.rounded"
    />
  </div>
</template>

<script setup>
import {ref, defineProps} from 'vue'
import Button from 'primevue/button';

// const plusBtnProps = defineProps({
//   severity :{
//     type: String,
//     required: false,
//     default: 'Primary',
//   },
//   icon :{
//   type: String,
//   required: false,
//   },
//   label :{
//   type: String,
//   required: false,
//   },
//   disabled : {
//     type: Boolean,
//     required: false,
//     default: false
//   },
//   raised : {
//     type: Boolean,
//     required: false,
//     default: false
//   },
//   rounded : {
//     type: Boolean,
//     required: false,
//     default: false
//   },
//   textMode : {
//     type: Boolean,
//     required: false,
//     default: false
//   },
//   outlined : {
//     type: Boolean,
//     required: false,
//     default: false
//   }
// })

const plusBtnProps = defineProps(['severity', 'icon', 'raised', 'rounded'])

</script>

<style scoped>

</style>