<template>
  <div class="card">
    <Select v-model="selectedOption"
            :options="propsOptions"
            :v-value="selectedOption"
            :filter="props.filter"
            variant="filled"
            :optionLabel="props.optionLabel"
            :placeholder="props.placeholder"
            @change="$emit('selectedOption', selectedOption.id)"
            class="w-full lg:w-48 " />
  </div>
</template>

<script setup>
import {ref, defineProps} from 'vue'
import Select from 'primevue/select';

const props = defineProps(['filter', 'options', 'optionLabel', 'placeholder'])
const selectedOption = ref('');
let propsOptions = props.options;


</script>

<style >
.p-select-option{
  direction: rtl;
}
.p-inputtext{
  direction: rtl;
}
</style>
