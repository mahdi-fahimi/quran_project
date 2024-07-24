<template>
  <div class="" id="search-input">
    <InputGroup>
      <InputText
          placeholder="جستجو ..."
          class="direction-rtl"
          v-model="searchInput"
          @keyup.enter="$emit('search', searchInput)"
      />
      <Button
          icon="pi pi-search"
          severity="primary"
          @click="$emit('search', searchInput)"
      />
    </InputGroup>
  </div>
</template>

<script setup >
import InputGroup from 'primevue/inputgroup';
import Button from 'primevue/button';
import InputText from 'primevue/inputtext';
import {ref} from "vue";

const searchInput = ref('')

</script>

<style scoped>
  #search-input{
    direction: ltr ;
  }
</style>