<template>
  <div id="img-border" class="container ">
    <div id="title" class="mb-4">
      <p class="UthmanicHafs1-font text-3xl"> الفاتحه </p>
    </div>
    <div id="sura-text" v-for="(aya, index) in text" :key="index">
        <div id="aya">
<!--          {{ aya.aya_number }}-->
          <p class="UthmanicHafs1-font text-2xl">
            {{ aya.main_text }}
          </p>
          <br>
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
</template>

<script setup lang="ts">
import {ref} from "vue"
import Divider from 'primevue/divider';

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
console.log(text)

</script>

<style scoped>
#img-border {
  border: 100px solid transparent;
  padding: 15px;
  border-image: url(../assets/images/border1.png) 360 round;
  direction: rtl;
  margin: 0;
}

#img-border #title{
  border: 25px solid black;
  border-image: url(../assets/images/border2.png) 106 round;
  width: 10rem;
  padding: 0.5rem;
}
</style>