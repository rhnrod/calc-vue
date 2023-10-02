<script setup>
import { reactive, ref } from 'vue';

const state = reactive({
  n1: 0,
  n2: 0,
  ref: ref('somar'),
  result: function () {
    switch (state.ref) {
      case 'subtrair':
        return state.n1 - state.n2
      case 'multiplicar':
        return state.n1 * state.n2
      case 'dividir':
        return state.n1 / state.n2
      default:
        return state.n1 + state.n2
    } 
  }
});

function changeNumber(e) {
  let num = e.target.id;

  switch (num) {
    case 'n1':
      return state.n1 = Number(e.target.value)
    case 'n2':
      return state.n2 = Number(e.target.value)
  }
}

function checkNumberLength() {
  let alpha =  Number(state.result().toString().length) >= 12;
  return alpha;
}

function checkNumberLength2() {
  let alpha =  Number(state.result().toString().length) >= 15;
  return alpha;
}

</script>

<template>
  <div class="container">
    <div class="row d-flex justify-content-center">
      <div class="col-8 mt-5 mb-5 d-flex showcase justify-content-end align-items-end">
        <h1 class="showcase__title">Vue calculator</h1>
        <span :class="{less: checkNumberLength(), lesser: checkNumberLength2()}" class="showcase__number">{{ state.result() }}</span>
      </div>
    </div>
    <div class="row d-flex justify-content-center">
      <div class="col-3">
        <input type="number" id="n1" @change="changeNumber" @keyup="changeNumber" :placeholder="state.n1" class="form-control">
      </div>
      <div class="col-3">
        <input type="number" id="n2" @change="changeNumber" @keyup="changeNumber" :placeholder="state.n2"  class="form-control">
      </div>
      <div class="col-2">
          <select class="form-select" v-model="state.ref">
            <option value="somar">somar</option>
            <option value="subtrair">subtrair</option>
            <option value="multiplicar">multiplicar</option>
            <option value="dividir">dividir</option>
          </select>
        </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  margin: 0 auto;
}
.showcase {
  height: 25vh;
  background-color: #282828;
  border-radius: 12px;
  position: relative;
}

.showcase__title {
  position: absolute;
  font-size: 12px;
  color: #ff9100;
  text-transform: uppercase;
  top: 10%;
  right: 2%;
}
.showcase__number {
  font-size: 100px;
  color: #fefefefe;
  transition: all ease 1s;
}

.form-control {
  font-size: 28px;
  background-color: #ececec;
}

.form-select {
  height: 56px;
  font-size: 22px;
  font-weight: bold;
  background-color: rgb(207, 110, 74);
  color: #fefefefe
}

.less {
  font-size: 82px;
}

.lesser {
  font-size: 56px;
}
</style>
