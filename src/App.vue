<template>
  <div id="app">
    <h1>Калькулятор</h1>
    <div class="calc">
      <div v-show="!end" class="inputs">
        <input type="text" v-model="firstValue">
        <input type="text" v-model="secondValue">
      </div>
      <div v-show="end" class="answer">
        <button @click="end = !end"><i class="fas fa-undo-alt"></i></button>
        <span>{{ result }}</span>
      </div>
      <div class="actions">
        <button class="action" @click="plus"><i class="fas fa-plus"></i></button>
        <button class="action" @click="minus"><i class="fas fa-minus"></i></button>
        <button class="action" @click="division"><i class="fas fa-divide"></i></button>
        <button class="action" @click="mult"><i class="fas fa-times"></i></button>
        <button class="action" @click="exp"><i class="fas fa-superscript"></i></button>
        <button class="action" @click="divisionWithoutRem"><i class="fas fa-divide"></i><br>
        <span>без ост</span></button>
      </div>
      
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      firstValue: '',
      secondValue: '',
      result: '',
      action: '',
      end: false
    }
  },
  methods: {
    plus() {
      this.result = +this.firstValue + +this.secondValue;
      this.end = true;
    },
    minus() {
      this.result = +this.firstValue - +this.secondValue;
      this.end = true;
    },
    mult() {
      this.result = +this.firstValue * +this.secondValue;
      this.end = true;
    },
    division() {
      this.result = +this.firstValue / +this.secondValue;
      this.end = true;
    },
    exp() {
      this.result = (+this.firstValue) ** +this.secondValue;
      this.end = true;
    },
    divisionWithoutRem() {
      this.result = Math.floor(+this.firstValue / +this.secondValue);
      this.end = true;
    }
  },
}
</script>
