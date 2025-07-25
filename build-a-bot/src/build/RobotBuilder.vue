<!-- eslint-disable no-const-assign -->
<template>
<div class="content">
  <button class="add-to-cart" @click="addToCart()">Add to Cart</button>
  <div class="top-row">
    <div class="top part" :class="{ 'sale-border': selectedRobot.head.onSale }">
      <div class="robot-name">{{ selectedRobot.head.title }}
      <span v-if="selectedRobot.head.onSale" class="sale">Sale!</span>
      </div>
      <img :src="selectedRobot.head.imageUrl" alt="head" />
      <button @click="selectPreviousHead()" class="prev-selector">&#9668;</button>
      <button @click="selectNextHead()" class="next-selector">&#9658;</button>
    </div>
  </div>
  <div class="middle-row">
    <div class="left part">
      <img :src="selectedRobot.leftArm.imageUrl" alt="left arm" />
      <button @click="selectPreviousLeftArm()"  class="prev-selector">&#9650;</button>
      <button @click="selectNextLeftArm()" class="next-selector">&#9660;</button>
    </div>
    <div class="center part">
      <img :src="selectedRobot.torso.imageUrl" alt="torso" />
      <button @click="selectPreviousTorso()"  class="prev-selector">&#9668;</button>
      <button @click="selectNextTorso()" class="next-selector">&#9658;</button>
    </div>
    <div class="right part">
      <img :src="selectedRobot.rightArm.imageUrl" alt="right arm" />
      <button @click="selectPreviousRightArm()"  class="prev-selector">&#9650;</button>
      <button @click="selectNextRightArm()" class="next-selector">&#9660;</button>
    </div>
  </div>
  <div class="bottom-row">
    <div class="bottom part">
      <img :src="selectedRobot.base.imageUrl" alt="base" />
      <button @click="selectPreviousBase()" class="prev-selector">&#9668;</button>
      <button @click="selectNextBase()" class="next-selector">&#9658;</button>
    </div>
  </div>
</div>
<div>
  <h1>Cart</h1>
    <table>
      <thead>
        <tr>
        <th>Robot</th>
        <th class="cost">Cost</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(robot, index) in cart" :key="index">
          <td>{{ robot.head.title }}</td>
          <td class="cost">{{ toCurrency(robot.cost) }}</td>
        </tr>
      </tbody>
    </table>
</div>
</template>

<script setup>
import { computed, ref } from 'vue';
import parts from '../data/parts';
import { toCurrency } from '../shared/formatters';

function getNextValidIndex(index, lenght) {
  const incrementedIndex = index + 1;
  return incrementedIndex > lenght - 1 ? 0 : incrementedIndex;
}

function getPreviousValidIndex(index, lenght) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? lenght - 1 : deprecatedIndex;
}

const availableParts = parts;
const selectedHeadIndex = ref(0);
const selectedLeftArmIndex = ref(0);
const selectedTorsoIndex = ref(0);
const selectedRightArmIndex = ref(0);
const selectedBaseIndex = ref(0);
const cart = ref([]);

const selectedRobot = computed(() => ({
  head: availableParts.heads[selectedHeadIndex.value],
  leftArm: availableParts.arms[selectedLeftArmIndex.value],
  torso: availableParts.torsos[selectedTorsoIndex.value],
  rightArm: availableParts.arms[selectedRightArmIndex.value],
  base: availableParts.bases[selectedBaseIndex.value],
}));

const addToCart = () => {
  const robot = selectedRobot.value;
  const cost = robot.head.cost +
    robot.leftArm.cost +
    robot.torso.cost +
    robot.rightArm.cost + robot.base.cost;
  cart.value.push({ ...robot, cost });
  console.log(cart.value.length);
};
const selectNextHead = () => {
  // eslint-disable-next-line no-const-assign
  selectedHeadIndex.value = getNextValidIndex(
    selectedHeadIndex.value,
    availableParts.heads.length,
  );
};
const selectPreviousHead = () => {
  // eslint-disable-next-line no-const-assign
  selectedHeadIndex.value = getPreviousValidIndex(
    selectedHeadIndex.value,
    availableParts.heads.length,
  );
};
const selectNextLeftArm = () => {
  // eslint-disable-next-line no-const-assign
  selectedLeftArmIndex.value = getNextValidIndex(
    selectedLeftArmIndex.value,
    availableParts.arms.length,
  );
};
const selectPreviousLeftArm = () => {
  // eslint-disable-next-line no-const-assign
  selectedLeftArmIndex.value = getPreviousValidIndex(
    selectedLeftArmIndex.value,
    availableParts.arms.length,
  );
};
const selectNextTorso = () => {
  // eslint-disable-next-line no-const-assign
  selectedTorsoIndex.value = getNextValidIndex(
    selectedTorsoIndex.value,
    availableParts.torsos.length,
  );
};
const selectPreviousTorso = () => {
  // eslint-disable-next-line no-const-assign
  selectedLeftArmIndex.value = getPreviousValidIndex(
    selectedLeftArmIndex.value,
    availableParts.torsos.length,
  );
};
const selectNextRightArm = () => {
  // eslint-disable-next-line no-const-assign
  selectedRightArmIndex.value = getNextValidIndex(
    selectedRightArmIndex.value,
    availableParts.arms.length,
  );
};
const selectPreviousRightArm = () => {
  // eslint-disable-next-line no-const-assign
  selectedRightArmIndex.value = getPreviousValidIndex(
    selectedRightArmIndex.value,
    availableParts.arms.length,
  );
};
const selectNextBase = () => {
  // eslint-disable-next-line no-const-assign
  selectedBaseIndex.value = getNextValidIndex(
    selectedBaseIndex.value,
    availableParts.bases.length,
  );
};
const selectPreviousBase = () => {
  // eslint-disable-next-line no-const-assign
  selectedBaseIndex.value = getPreviousValidIndex(
    selectedBaseIndex.value,
    availableParts.bases.length,
  );
};
</script>

<style scoped>
.part {
  position: relative;
  width: 200px;
  height: 200px;
  border: 3px solid #aaa;
}

.sale-border {
  border: 3px solid red;
}

.part img {
  width: 200px;
}

.top-row {
  display: flex;
  justify-content: space-around;
}

.middle-row {
  display: flex;
  justify-content: center;
}

.bottom-row {
  display: flex;
  justify-content: space-around;
  border-top: none;
}

.top {
  border-bottom: none;
}

.left {
  border-right: none;
}

.right {
  border-left: none;
}

.left img {
  transform: rotate(-90deg);
}

.right img {
  transform: rotate(90deg);
}

.bottom {
  border-top: none;
}

.prev-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 206px;
}

.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 206px;
}

.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}

.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 179px;
  height: 25px;
}

.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 179px;
  height: 25px;
}

.right .next-selector {
  right: -3px;
}

.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}

.sale {
  color: red;
}

.content {
  position: relative;
}

.add-to.cart {
  position: absolute;
  right: 30px;
  width: 220px;
  padding: 3px;
  font-size: 16px;}

td,
th {
  text-align: left;
  padding: 5px;
  padding-right: 20px;
}

.cost{
  text-align: right;
}
</style>
