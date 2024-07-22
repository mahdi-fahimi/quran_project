<template>
  <div class="card">
    <Select v-model="selectedOption"
            :options="propsOptions"
            :v-value="selectedOption"
            :filter="props.filter"
            variant="filled"
            :optionLabel="props.optionLabel"
            class="w-full md:w-36 " />
  </div>
</template>

<script setup>
import {ref, defineProps} from 'vue'
import Select from 'primevue/select';

const props = defineProps(['filter', 'options', 'optionLabel'])
// const selectedOption = ref(props.options._rawValue[0].name);
// const selectedOption = ref(props.options);
const selectedOption = ref('');

let propsOptions = props.options;


</script>

<style scoped>
</style>
