<template>
  <div id="app">
    <h1>Калькулятор</h1>
    <div class="calc">
      <div style="display: none">
          <input type="radio" id="one" value='one' v-model="picked">
          <label for="one">Операнд 1</label> 
          <input type="radio" id="two" value='two' v-model="picked">
          <label for="two">Операнд 2</label>       
        </div>
      <div v-show="!end" class="inputs">
        <input type="text" @click="changeInputOne" v-model="value.one">
        <input type="text" @click="changeInputTwo" v-model="value.two">
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
        <button 
          v-show="checked" 
          v-for="(button, item) in buttons" 
          @click="addNumber(button)"
          :key="item">
            {{ button }}
          </button>
        <button @click="remove" v-show="checked"><i class="fas fa-backspace"></i></button>
        <button @click="clearInput" v-show="checked"><i class="fas fa-ban"></i></button>
        <input class="numberButton" type="checkbox" id="checkbox" v-model="checked">
        <label class="keyboard" for="checkbox"><i class="far fa-keyboard"></i></label>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      value: {
        'one': '',
        'two': '',
      },
      result: '',
      action: '',
      end: false,
      checked: false,
      buttons: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
      picked: true,
    }
  },
  methods: {
    clearInput() {
      this.value.one = '';
      this.value.two = '';
    },
    changeInputOne() {
      this.picked = 'one';
    },
    changeInputTwo() {
      this.picked = 'two';
    },
    remove() {
      this.value[this.picked] = this.value[this.picked].slice(0, this.value[this.picked].length - 1)
    },
    addNumber(num) {
      this.value[this.picked] = this.value[this.picked] + num;
    },
    plus() {
      this.result = +this.value.one + +this.value.two;
      this.end = true;
    },
    minus() {
      this.result = +this.value.one - +this.value.two;
      this.end = true;
    },
    mult() {
      this.result = +this.value.one * +this.value.two;
      this.end = true;
    },
    division() {
      if(this.value.two != false) {
        this.result = +this.value.one / +this.value.two;
      } else {
        this.result = 'На 0 делить нельзя'
      }
      
      this.end = true;
    },
    exp() {
      this.result = (+this.value.one) ** +this.value.two;
      this.end = true;
    },
    divisionWithoutRem() {
      if(this.value.two != false) {
        this.result = Math.floor(+this.value.one / +this.value.two);
      } else {
        this.result = 'На 0 делить нельзя'
      }
      
      this.end = true;
    },
  },
}
</script>
