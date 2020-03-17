/*
  refs.
  乗算
  https://lab.syncer.jp/Web/JavaScript/Snippet/16/
  小数桁指定切り上げ
  https://qiita.com/nagito25/items/0293bc317067d9e6c560
 */
<template>
  <div class="content">
    height: <input type="text" v-model="height" /> cm
    weight: <input type="text" v-model="weight" /> kg
    <p>{{ height }}, {{ weight }}</p>
    <button @click="calc">BMIを計算！</button>
    <p>あなたのBMIは {{ bmi }} です。</p>
  </div>
</template>

<script>
export default {
  name: 'Main',
  data() {
    return {
      height: "",
      weight: "",
      bmi: "",
    }
  },
  methods: {
    calc(event) {
      if (!this.height) {
        console.log("Height is empty");
        return;
      }
      if (!this.weight) {
        console.log("Weight is empty");
        return;
      }
      this.bmi = +this.weight / Math.pow(+this.height / 100, 2);
      this.bmi = Math.round(this.bmi * 10) / 10;
    },
  }
}
</script>

<style>
</style>
