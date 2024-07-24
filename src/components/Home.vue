<template >
  <div class="mt-6 relative">
<!--  drop downs -->
    <div class="flex gap-4 direction-rtl max-w-[87%] mx-auto my-4">
      <!-- select sura -->
      <SelectDropDown
      :options="selectSuraProps.allSuraNames"
      :filter="selectSuraProps.filter"
      :optionLabel="selectSuraProps.optionLabel"
      :placeholder="selectSuraProps.placeholder"
      @selectedOption="receiveSuraDropdownEmit"
      />
      <!-- select translation -->
      <SelectDropDown
      :options="selectTranslationProps.allTranslatorsNames"
      :filter="selectTranslationProps.filter"
      :optionLabel="selectTranslationProps.optionLabel"
      :placeholder="selectTranslationProps.placeholder"
      @selectedOption="receiveTranslatorDropdownEmit"
      />
      <SearchInput
          @search="receiveSearchInputEmit"
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
        <p class="uthmanTaha-font text-3xl text-center ">
          {{ suraName.sura }}
        </p>
      </div>
<!--   بسم الله   -->
      <div v-if="suraNumber !== 9" class="text-center mt-8">
        <p  class="uthmanTaha-font text-2xl mb-4">
          بِسْمِ اللَّهِ الرَّحْمَـٰنِ الرَّحِيمِ
        </p>
        <p v-if="translatorId === 1" class="text-lg mb-4">
          In the name of Allah, Most Gracious, Most Merciful
        </p>
        <p v-else-if="translatorId === 2" class="vazir-font text-lg mb-4">
          به نام خداوند بخشنده مهربان
        </p>
        <p v-else class="vazir-font text-lg mb-4">
          ستایش مخصوص خداوندی است که پروردگار جهانیان است
        </p>
        <Divider/>
      </div>

      <div id="sura-text" v-for="(aya, index) in allAyaText" :key="index">
        <div v-if="aya !== 'بِسْمِ اللَّهِ الرَّحْمَـٰنِ الرَّحِيمِ' ">
          <div id="aya" >
            <p  class="uthmanTaha-font text-2xl leading-[4rem] inline text-justify " >
              {{ aya }}
            </p>
            <div id="aya-number" class="inline-flex items-center mr-2 align-middle">
              <img src="https://upload.wikimedia.org/wikipedia/commons/6/69/Ra_bracket.png"
                   alt="bracket"
                   class="w-3"
              >
              <span  class="vazir-font mx-1 text-lg">
              {{ allAyaNumber[index] }}
            </span>
              <img src="https://upload.wikimedia.org/wikipedia/commons/1/18/La_bracket.png"
                   alt="bracket"
                   class="w-3"
              >
            </div>
          </div>
          <div id="translation">
            <p v-if="suraNumber === 1"
               class="vazir-font text-lg leading-9 text-justify"
               :class="{'direction-ltr' : translatorId === 1  }">
              {{ allTranslation[index-1] }}
            </p>
            <p v-else
               class="vazir-font text-lg leading-9 text-justify"
               :class="{'direction-ltr' : translatorId === 1}">
              {{ allTranslation[index] }}
            </p>
          </div>
          <div v-if="index !== allAyaText.length-1">
            <Divider/>
          </div>
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
import SearchInput from "./SearchInput.vue";

const allAyaText =ref( [])
const allAyaNumber =ref( [])
const allTranslation =ref( [])
const suraName = ref('بقره')
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
  optionLabel: 'sura',
  placeholder: 'انتخاب سوره'
}
const selectTranslationProps = {
  filter : false,
  allTranslatorsNames,
  optionLabel: 'translator',
  placeholder: 'انتخاب ترجمه'
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
        allAyaText.value = ayaOfSura.data;
        allAyaNumber.value = ayaOfSura.ayaNumberArray
      })
  // get translation
  fetch(`http://localhost:3000/translation/${translatorId.value}&${suraNumber}`)
      .then(response => {
        return response.json();
      })
      .then(ayaOfSura => {
        allTranslation.value = ayaOfSura.data;
      })
  // get sura name
  fetch(`http://localhost:3000/sura/${suraNumber}`)
      .then(response => {
        return response.json();
      })
      .then(ayaOfSura => {
        suraName.value = ayaOfSura.data;
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

function receiveSearchInputEmit(value){
  fetch(`http://localhost:3000/search/${value}`)
      .then(response => {
        return response.json();
      })
      .then(searchResult => {
        allAyaText.value = searchResult.data;
        console.log(allAyaText.value)
      })
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

#abc{
  direction: ltr !important;
}
</style>