<template >
  <div class="mt-6 relative">
    <div class="flex gap-4 direction-rtl max-w-[87%] mx-auto my-4">
      <!-- select sura -->
      <SelectDropDown
      :options="selectSuraProps.allSuraNames"
      :filter="selectSuraProps.filter"
      />
      <!-- select translation -->
      <SelectDropDown
      :options="selectTranslationProps.allTranslatorsNames"
      :filter="selectTranslationProps.filter"
      />
    </div>
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
    <div id="main-box" class="max-w-[90%] mx-auto direction-rtl">
      <div id="sura-name" class="mb-4 text-center mx-auto w-40 p-2" >
        <p class="uthmanTaha-font text-3xl text-center"> الفاتحه </p>
      </div>
      <div id="sura-text" v-for="(aya, index) in text" :key="index">
        <div id="aya" class="flex gap-2">
          <p class="uthmanTaha-font text-2xl mb-4">
            {{ aya.main_text }}
          </p>
          <div id="aya-number" class="flex items-center">
            <img src="https://upload.wikimedia.org/wikipedia/commons/6/69/Ra_bracket.png"
                 alt="bracket"
                 class="w-3"
            >
            <span class="vazir-font mx-1 text-lg">
              {{ aya.aya_number }}
            </span>
            <img src="https://upload.wikimedia.org/wikipedia/commons/1/18/La_bracket.png"
                 alt="bracket"
                 class="w-3"
            >
          </div>
        </div>
        <div id="translation">
          <p class="vazir-font text-lg">
            {{ aya.translation }}
          </p>
        </div>
        <div v-if="index !== text.length-1">
          <Divider/>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue"
import Divider from 'primevue/divider';
import Btn from './Btn.vue'
import SelectDropDown from "./SelectDropDown.vue";

let text =ref( [
  {
    id : 1,
    sura_number : 1,
    aya_number : 1,
    main_text : 'بِسْمِ اللَّهِ الرَّحْمَـٰنِ الرَّحِيمِ',
    translation : 'به نام خداوند رحمتگر مهربان'
  },
  {
    id : 2,
    sura_number : 1,
    aya_number : 2,
    main_text : 'الْحَمْدُ لِلَّهِ رَبِّ الْعَالَمِينَِ',
    translation : 'ستایش خدایی را که پروردگار جهانیان'
  },
  {
    id : 3,
    sura_number : 1,
    aya_number : 3,
    main_text : 'الرَّحْمَـٰنِ الرَّحِيمَِِ',
    translation : 'رحمتگر مهربان'
  },
  {
    id : 4,
    sura_number : 1,
    aya_number : 4,
    main_text : 'مَالِكِ يَوْمِ الدِّينَِِِ',
    translation : '[و] خداوند روز جزاست'
  },
  {
    id : 5,
    sura_number : 2,
    aya_number : 0,
    main_text : 'بِسْمِ اللَّهِ الرَّحْمَـٰنِ الرَّحِيمِ',
    translation : 'به نام خداوند رحمتگر مهربان'
  },
  {
    id : 6,
    sura_number : 2,
    aya_number : 1,
    main_text : 'المِ',
    translation : 'الف، لام، میم'
  },
  {
    id : 7,
    sura_number : 2,
    aya_number : 2,
    main_text : 'ذَٰلِكَ الْكِتَابُ لَا رَيْبَ ۛ فِيهِ ۛ هُدًى لِّلْمُتَّقِينَِ',
    translation : 'این است کتابی که در [حقانیت‌] آن هیچ تردیدی نیست؛ [و] مایه هدایت تقواپیشگان است'
  },
  {
    id : 8,
    sura_number : 2,
    aya_number : 3,
    main_text : 'الَّذِينَ يُؤْمِنُونَ بِالْغَيْبِ وَيُقِيمُونَ الصَّلَاةَ وَمِمَّا رَزَقْنَاهُمْ يُنفِقُونَِ',
    translation : 'آنان که به غیب ایمان می‌آورند، و نماز را بر پا می‌دارند، و از آنچه به ایشان روزی داده‌ایم انفاق می‌کنند؛'
  },
  {
    id : 9,
    sura_number : 2,
    aya_number : 4,
    main_text : 'وَالَّذِينَ يُؤْمِنُونَ بِمَا أُنزِلَ إِلَيْكَ وَمَا أُنزِلَ مِن قَبْلِكَ وَبِالْآخِرَةِ هُمْ يُوقِنُونَِ',
    translation : 'و آنان که بدانچه به سوی تو فرود آمده، و به آنچه پیش از تو نازل شده است، ایمان می آورند؛ و آنانند که به آخرت یقین دارند.'
  },
  {
    id : 10,
    sura_number : 2,
    aya_number : 5,
    main_text : 'أُولَـٰئِكَ عَلَىٰ هُدًى مِّن رَّبِّهِمْ ۖ وَأُولَـٰئِكَ هُمُ الْمُفْلِحُونَِ',
    translation : 'آنان برخوردار از هدایتی از سوی پروردگار خویشند؛ و آنان همان رستگارانند.'
  },
  {
    id : 11,
    sura_number : 2,
    aya_number : 6,
    main_text : 'إِنَّ الَّذِينَ كَفَرُوا سَوَاءٌ عَلَيْهِمْ أَأَنذَرْتَهُمْ أَمْ لَمْ تُنذِرْهُمْ لَا يُؤْمِنُونَِ',
    translation : 'در حقیقت کسانی که کفر ورزیدند -چه بیمشان دهی، چه بیمشان ندهی- بر ایشان یکسان است؛ [آنها] نخواهند گروید.'
  },
  {
    id : 12,
    sura_number : 3,
    aya_number : 0,
    main_text : 'بِسْمِ اللَّهِ الرَّحْمَـٰنِ الرَّحِيمِ',
    translation : 'به نام خداوند رحمتگر مهربان'
  },
  {
    id : 13,
    sura_number : 3,
    aya_number : 1,
    main_text : 'قُلْ أَعُوذُ بِرَبِّ النَّاسِ',
    translation : 'بگو: «پناه می‌برم به پروردگار مردم،'
  },
  {
    id : 14,
    sura_number : 3,
    aya_number : 2,
    main_text : 'مَلِكِ النَّاسِ',
    translation : 'پادشاه مردم،'
  },
  {
    id : 15,
    sura_number : 3,
    aya_number : 3,
    main_text : 'المِ',
    translation : 'الف، لام، میم'
  },{
    id : 16,
    sura_number : 3,
    aya_number : 4,
    main_text : 'إِلَـٰهِ النَّاسِِ',
    translation : 'معبود مردم،'
  },
])
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
const allSuraNames = ref([
  {number : 1, name : 'الفاتحه'},
  {number : 2, name : 'البقره'},
  {number : 3, name : 'آل عمران'},
  {number : 4, name : 'النساء'},
  {number : 5, name : 'الفاتحه'},
  {number : 6, name : 'الفاتحه'},
  {number : 7, name : 'الفاتحه'},
  {number : 8, name : 'الفاتحه'},
  {number : 9, name : 'الفاتحه'},
])
const allTranslatorsNames = ref([
  {number: 1, name: 'یوسف علی'},
  {number: 2, name: 'فولادوند'},
  {number: 3, name: 'مکارم'},
])
const selectSuraProps = {
  filter : true,
  allSuraNames
}
const selectTranslationProps = {
  filter : false,
  allTranslatorsNames
}

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