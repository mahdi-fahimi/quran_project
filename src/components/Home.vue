<template class="abc">
  <div class="mt-6 relative ">
<!--  drop downs -->
    <div class="flex flex-wrap gap-4 direction-rtl max-w-[87%] mx-auto my-4">
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
      <div v-if="isSearching">
        <p  class="vazir-font  leading-9 text-justify">
          {{allAyaText.length}} نتیجه یافت شد.
        </p>
      </div>
    </div>

<!--  btns  -->
    <div class="fixed top-72 left-4 flex flex-col gap-2">
      <Btn :severity="plusBtnProps.severity"
           :icon="plusBtnProps.icon"
           :raised="plusBtnProps.raised"
           :rounded="plusBtnProps.rounded"
           @click="changeFontSize('+', 2)"
           :title="arabicFontSize"
      />
      <Btn :severity="minusBtnProps.severity"
           :icon="minusBtnProps.icon"
           :raised="minusBtnProps.raised"
           :rounded="minusBtnProps.rounded"
           @click="changeFontSize('-', 2)"
           :title="arabicFontSize"
      />
    </div>
<!--  aya and translation  -->
    <div id="main-box" class="lg:max-w-[90%] mx-auto direction-rtl">
<!--   sura name   -->
      <div v-if="!isSearching" id="sura-name" class="mb-4 text-center mx-auto w-40 p-2" >
        <p class="uthmanTaha-font text-3xl text-center ">
          {{ suraName.sura }}
        </p>
      </div>
      <div v-if="suraNumber !== 9 && !isSearching" class="text-center mt-8">
        <p  class="uthmanTaha-font mb-4 arabic-font-size">
          بِسْمِ اللَّهِ الرَّحْمَـٰنِ الرَّحِيمِ
        </p>
        <p v-if="translatorId === 1" class="mb-4 translation-font-size">
          In the name of Allah, Most Gracious, Most Merciful
        </p>
        <p v-else-if="translatorId === 2" class="vazir-font mb-4 translation-font-size">
          به نام خداوند بخشنده مهربان
        </p>
        <p v-else class="vazir-font mb-4 translation-font-size">
          ستایش مخصوص خداوندی است که پروردگار جهانیان است
        </p>
        <Divider/>
      </div>

      <div v-if="allAyaText" id="sura-text" v-for="(aya, index) in allAyaText" :key="index">
        <div v-if="aya !== 'بِسْمِ اللَّهِ الرَّحْمَـٰنِ الرَّحِيمِ' ">
          <div id="aya" >
            <span v-if="isSearching" class="vazir-font translation-font-size leading-[4rem] inline text-justify">
              {{++index}} -
            </span>
            <p  class="uthmanTaha-font arabic-font-size leading-[4rem] inline text-justify " >
              {{ aya }}
            </p>
            <div id="aya-number"
                 class="inline-flex items-center mr-2 align-middle "
                 :class="{'text-red-800' : isSearching}">
              <img src="https://upload.wikimedia.org/wikipedia/commons/6/69/Ra_bracket.png"
                   alt="bracket"
                   class="w-3"
              >
              <span v-if="isSearching" class="uthmanTaha-font mx-1 translation-font-size">
               {{ allSuraNameSearch[index] }}
              </span>
              <span  class="vazir-font mx-1 translation-font-size">
                {{ allAyaNumber[index] }}
              </span>
              <img src="https://upload.wikimedia.org/wikipedia/commons/1/18/La_bracket.png"
                   alt="bracket"
                   class="w-3"
              >
              <div v-if="isSearching"
                   class="mr-2 bg-gray-300 text-white py-1 px-2 rounded-full hover:bg-black transition ease-in-out cursor-pointer"
                   @click="changeSura(allSuraNumberSearch[index])"
              >
                <i class="pi pi-arrow-left"></i>
              </div>
            </div>
          </div>
          <div id="translation">
            <p v-if="suraNumber === 1"
               class="vazir-font translation-font-size leading-9 text-justify"
               :class="{'direction-ltr' : translatorId === 1  }">
              {{ allTranslation[index-1] }}
            </p>
            <p v-if="isSearching || suraNumber !== 1"
               class="vazir-font translation-font-size leading-9 text-justify"
               :class="{'direction-ltr' : translatorId === 1}">
              {{ allTranslation[index] }}
            </p>
          </div>
          <div v-if="index !== allAyaText.length-1">
            <Divider/>
          </div>
        </div>
      </div>
      <div v-if="allAyaText.length === 0">
        <p class="vazir-font translation-font-size leading-9 text-justify">
          نتیجه ای یافت نشد
        </p>
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
const allSuraName = ref([])
const allSuraNameSearch = ref([])
const allSuraNumberSearch = ref([])
const allSuraNames = ref([])
const allTranslatorsNames = ref([])
const suraNumber = ref(1)
const translatorId = ref(2)
const isSearching = ref(false)
const searchedText = ref('')
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
const arabicFontSize = ref(24)
const translationFontSize = ref(18)
const translationFontSizeString = ref(`${translationFontSize.value}px`)
const arabicFontSizeString = ref(`${arabicFontSize.value}px`)

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
      .then(allSuras => {
        allSuraNames.value = allSuras.data;
        allSuraNameSearch.value.forEach((suraNumber) => {
          let suraName = allSuraNames[suraNumber];
          allSuraName.value.push(suraName);
        })
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
      .then(result => {
        suraName.value = result.data;
      })
}

function receiveSuraDropdownEmit(value){
  isSearching.value = false
  suraNumber.value = value
  getAya(suraNumber.value)
}

function receiveTranslatorDropdownEmit(value){
  translatorId.value = value
  if(isSearching.value){
    getTranslation(value,allSuraNumberSearch.value,allAyaNumber.value)
  } else {
    getAya(suraNumber.value)
  }
}

function receiveSearchInputEmit(value){
  isSearching.value = true;
  searchedText.value = value
  allTranslation.value = []
  fetch(`http://localhost:3000/search/${value}`)
      .then(response => {
        return response.json();
      })
      .then(searchResult => {
        allAyaText.value = searchResult.searchTextArray
        allAyaNumber.value = searchResult.data
        allSuraNameSearch.value = searchResult.searchSuraNameArray
        allSuraNumberSearch.value = searchResult.searchSuraNumberArray
        getTranslation(translatorId.value,allSuraNumberSearch.value,allAyaNumber.value)
      })
}

function changeSura(value){
  if(isSearching.value){
    isSearching.value = false
    suraNumber.value = value
    getAya(suraNumber.value)
  }
}

function getTranslation(translatorId, surahNumber, ayaNumber){
  for(let i = 0; i < surahNumber.length; i++){
    fetch(`http://localhost:3000/translation/${translatorId}/${surahNumber[i]}/${ayaNumber[i]}`)
        .then(response => {
          return response.json();
        })
        .then(result => {
          allTranslation.value.push(result.data[0])
        })
  }
}

function changeFontSize(operator , n){
  if(operator === '+' && arabicFontSize.value < 50){
    arabicFontSize.value += n;
    translationFontSize.value += n;
  }
  if(operator === '-' && translationFontSize.value > 10){
    arabicFontSize.value -= n;
    translationFontSize.value -= n;
  }
  translationFontSizeString.value = `${translationFontSize.value}px`;
  arabicFontSizeString.value =`${arabicFontSize.value}px`;
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

.arabic-font-size{
  font-size: v-bind(arabicFontSizeString);
}
.translation-font-size{
  font-size: v-bind(translationFontSizeString);
}

.abc{
  background-image: url("../assets/images/11.jpg");
}

</style>