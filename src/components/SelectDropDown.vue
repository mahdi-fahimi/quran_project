<template>
  <div class="card">
    <Select v-model="selectedOption"
            :options="propsOptions"
            :v-value="selectedOption"
            :filter="props.filter"
            variant="filled"
            :optionLabel="props.optionLabel"
            @change="$emit('selectedOption', selectedOption.id)"
            class="w-full md:w-36 " />
  </div>
</template>

<script setup>
import {ref, defineProps} from 'vue'
import Select from 'primevue/select';

const props = defineProps(['filter', 'options', 'optionLabel'])
const selectedOption = ref('');
let propsOptions = props.options;

</script>

<style scoped>
</style>
