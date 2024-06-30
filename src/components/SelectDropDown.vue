<template>
  <div class="card">
    <Select v-model="selectedOption"
            :options="props.options._rawValue"
            :v-value="selectedOption"
            :filter="props.filter"
            variant="filled"
            optionLabel="name"
            :placeholder="props.options._rawValue[0].name"
            class="w-full md:w-36 " />
  </div>
</template>

<script setup>
import {ref, defineProps} from 'vue'
import Select from 'primevue/select';

const props = defineProps(['filter', 'options'])
const selectedOption = ref(props.options._rawValue[0].name);
</script>

<style scoped>
</style>
