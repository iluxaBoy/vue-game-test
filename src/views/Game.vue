<script setup>
import { ref, onMounted } from "vue";
const X = ref(0);
const Y = ref(0);
const boxX = ref();
const boxY = ref();

const createBoxes = (element) => {
  const div = document.createElement("div");
  div.className = "hoverBox";
  div.style.width = "36px";
  div.style.height = "36px";
  div.style.backgroundColor = "white";

  div.addEventListener("mouseover", () => {
    div.style.backgroundColor = "blue";
  });
  div.addEventListener("mouseout", () => {
    div.style.backgroundColor = "white";
  });
  
  element.value.appendChild(div);
};

const showBoxes = (element, amount) => {
  let index = 0;

  let intervalId = null;
  intervalId = setInterval(() => {
    if (index !== amount) {
      createBoxes(element);
      index++;
    } else {
      clearInterval(intervalId);
      intervalId = null;
    }
  }, 200);
};

const submitXY = () => {
  showBoxes(boxX, Number(X.value));
  showBoxes(boxY, Number(Y.value));
};
</script>

<template>
  <v-container>
    <div>
      <v-sheet theme="dark" class="mx-auto" width="300">
        <v-form @submit.prevent="submitXY">
          <v-text-field type="number" v-model="X" label="X"></v-text-field>

          <v-text-field type="number" v-model="Y" label="Y"></v-text-field>

          <v-btn class="mt-2" type="submit" block>Submit </v-btn>
        </v-form>
      </v-sheet>
    </div>
    <div class="box mt-6">
      <div class="row" ref="boxX"></div>
      <div class="colom" ref="boxY"></div>
    </div>
  </v-container>
</template>

<style scoped lang="scss">
.box {
  height: 500px;
  .row {
    display: flex;
    flex-direction: row;
  }
  .colom {
    display: flex;
    flex-direction: column;
  }
}
.hover-box {
  margin: 12px;
}
.hoverBox:hover {
  background-color: blue;
}
</style>
