/*
  refs.
  乗算
  https://lab.syncer.jp/Web/JavaScript/Snippet/16/
  小数桁指定切り上げ
  https://qiita.com/nagito25/items/0293bc317067d9e6c560
  watch
  https://qiita.com/mizon-webdesign/items/501646818f44e431d131
  @input
  https://blog.capilano-fw.com/?p=2787
 */
<template>
  <div class="content">
    <div v-if="isInput">
      <ul>
        <li>
          身長 <input type="text" @input="onInputHeight" v-model="height" /> cm
        </li>
        <li class="errorText" v-if="heightError">
          身長を入力してください。
        </li>
        <li>
          体重 <input type="text" @input="onInputWeight" v-model="weight" /> kg
        </li>
        <li class="errorText" v-if="weightError">
          体重を入力してください。
        </li>
      </ul>
      <button @click="calc">BMIを計算！</button>
    </div>

    <div v-if="bmi">
      <p>あなたのBMIです。</p>
      <p id="bmi">{{ bmi }}</p>
      <p>あなたのデータ</p>
      <ul>
        <li>
          身長 {{ height }} cm
        </li>
        <li>
          体重 {{ weight }} kg
        </li>
      </ul>
      <p>{{ weight }} kg ÷ ({{ height_m }} m)<sup>2</sup></p>
      <button @click="prev">もう1度計算する</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Main',
  data() {
    return {
      height: "",
      height_m: "",
      weight: "",
      bmi: "",
      isInput: true,
      heightError: false,
      weightError: false,
    }
  },
  watch: {
    height: function(newVal, oldVal) {
      this.height_m = +this.height / 100
    }
  },
  methods: {
    check() {
      var isError = false;
      if (!this.height_m) {
        console.log("Height is empty");
        this.heightError = true;
        isError = true;
      }
      if (!this.weight) {
        console.log("Weight is empty");
        this.weightError = true;
        isError = true;
      }
      return isError;
    },
    calc(event) {
      if (this.check()) {
        return;
      };
      this.isInput = false;
      this.bmi = +this.weight / Math.pow(+this.height_m, 2);
      this.bmi = Math.round(this.bmi * 10) / 10;
    },
    onInputHeight() {
      this.heightError = false;
    },
    onInputWeight() {
      this.weightError = false;
    },
    init() {
      console.log("init");
      this.height = "";
      this.height_m = "";
      this.weight = "";
      this.bmi = "";
      this.isInput = true;
    },
    prev(event) {
      this.init();
    }
  }
}
</script>

<style>
.errorText {
  color: red;
  font-weight: bold;
}
#id {
  font-weight: bold;
}
</style>
