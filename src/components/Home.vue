<template >
  <div class="mt-6 relative">
<!--  drop downs -->
    <div class="flex gap-4 direction-rtl max-w-[87%] mx-auto my-4">
      <!-- select sura -->
      <SelectDropDown
      :options="selectSuraProps.allSuraNames"
      :filter="selectSuraProps.filter"
      :optionLabel="selectSuraProps.optionLabel"
      @selectedOption="receiveSuraDropdownEmit"
      />
      <!-- select translation -->
      <SelectDropDown
      :options="selectTranslationProps.allTranslatorsNames"
      :filter="selectTranslationProps.filter"
      :optionLabel="selectTranslationProps.optionLabel"
      @selectedOption="receiveTranslatorDropdownEmit"
      />
    </div>
<!--  btns  -->
    <div class="absolute top-72 left-4 flex flex-col gap-2">
      <Btn :severity="plusBtnProps.severity"
           :icon="plusBtnProps.icon"
           :raised="plusBtnProps.raised"
           :rounded="plusBtnProps.rounded"
      />
      <Btn :severity="minusBtnProps.severity"
           :icon="minusBtnProps.icon"
           :raised="minusBtnProps.raised"
           :rounded="minusBtnProps.rounded"
      />
    </div>
<!--  aya and translation  -->
    <div id="main-box" class="max-w-[90%] mx-auto direction-rtl">
<!--   sura name   -->
      <div id="sura-name" class="mb-4 text-center mx-auto w-40 p-2" >
        <p class="uthmanTaha-font text-3xl text-center"> الفاتحه </p>
      </div>

      <div id="sura-text" v-for="(aya, index) in allAya" :key="index">
        <div id="aya" class="flex gap-2">
          <p  class="uthmanTaha-font text-2xl mb-4">
            {{ aya }}
          </p>
          <div id="aya-number" class="flex items-center">
            <img src="https://upload.wikimedia.org/wikipedia/commons/6/69/Ra_bracket.png"
                 alt="bracket"
                 class="w-3"
            >
            <span  class="vazir-font mx-1 text-lg">
              {{ ++index }}
            </span>
            <img src="https://upload.wikimedia.org/wikipedia/commons/1/18/La_bracket.png"
                 alt="bracket"
                 class="w-3"
            >
          </div>
        </div>
        <div id="translation">
          <p class="vazir-font text-lg">
            {{ allTranslation[index-1] }}
          </p>
        </div>
        <div v-if="index !== allAya.length">
          <Divider/>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup >
import {ref} from "vue";
import Divider from 'primevue/divider';
import Btn from './Btn.vue'
import SelectDropDown from "./SelectDropDown.vue";

// {
//   id : 1,
//   sura_number : 1,
//   aya_number : 1,
//   main_text : 'بِسْمِ اللَّهِ الرَّحْمَـٰنِ الرَّحِيمِ',
//   translation : 'به نام خداوند رحمتگر مهربان'
// }

const allAya =ref( [])
const allTranslation =ref( [])
const allSuraNames = ref([])
const allTranslatorsNames = ref([])
const suraNumber = ref(1)
const translatorId = ref(2)
const plusBtnProps = {
  severity: "Primary",
  icon: "pi pi-plus",
  raised: true,
  rounded: true
}
const minusBtnProps = {
  severity: "Primary",
  icon: "pi pi-minus",
  raised: true,
  rounded: true
}
const selectSuraProps = {
  filter : true,
  allSuraNames,
  optionLabel: 'sura'
}
const selectTranslationProps = {
  filter : false,
  allTranslatorsNames,
  optionLabel: 'translator'
}

///////////////////////////////

function getAllSuraNames () {
  // try{
  //   let res = await fetch('http://localhost:3000/sura')
  //   if(res.ok){
  //     let sura = await res.json()
  //     console.log(sura)
  //   } else{
  //     console.log('there is no sura');
  //   }
  // }
  // catch(err){
  //   console.log(err)
  // }
  // fetch('https://jsonplaceholder.typicode.com/todos/1')
  fetch('http://localhost:3000/sura')
      .then(response => {
        return response.json();
      })
      // .then(A => console.log(A.data))
      .then(allSuras => {
        allSuraNames.value = allSuras.data;
      })

  fetch('http://localhost:3000/translators')
      .then(response => {
        return response.json();
      })
      .then(translators => {
        allTranslatorsNames.value = translators.data;
      })

}

function getAya (suraNumber){
  // get aya
  fetch(`http://localhost:3000/quran/${suraNumber}`)
      .then(response => {
        return response.json();
      })
      .then(ayaOfSura => {
        allAya.value = ayaOfSura.data;
      })
  // get translation
  fetch(`http://localhost:3000/translation/${translatorId.value}&${suraNumber}`)
      .then(response => {
        return response.json();
      })
      .then(ayaOfSura => {
        allTranslation.value = ayaOfSura.data;
      })
}

function receiveSuraDropdownEmit(value){
  suraNumber.value = value
  getAya(suraNumber.value)
}

function receiveTranslatorDropdownEmit(value){
  translatorId.value = value
  getAya(suraNumber.value)
}

getAllSuraNames()

getAya(suraNumber.value)

</script>

<style scoped>
#main-box {
  border: 100px solid transparent;
  border-image: url(../assets/images/border1.png) 360 round;
}

#main-box #sura-name{
  border: 25px solid transparent;
  border-image: url(../assets/images/border2.png) 106 round;
}
</style>