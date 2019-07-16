<template>
  <div class='content'>
    <button class='add-to-cart' @click="addToCart()">Add to cart</button>
    <div class="top-row">
      <div :class="[saleBorderCLass, 'top', 'part']">
        <div class="robot-name">
          {{selectedRobot.head.title}}
          <span v-show="selectedRobot.head.onSale" class='sale'>Sale!</span>
        </div>
        <img :src="selectedRobot.head.src" title="head" />
        <button @click="selectPreviousHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.leftArm.src" title="left arm" />
        <button @click="selectPreviousLeftArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextLeftArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torsos.src" title="left arm" />
        <button @click="selectTorsoPrevious()" class="prev-selector">&#9668;</button>
        <button @click="selectTorsoNext()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.src" title="left arm" />
        <button @click="selectPreviousRightArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextRightArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.bases.src" title="left arm" />
        <button @click="selectBasesPrevious()" class="prev-selector">&#9650;</button>
        <button @click="selectBasesNext()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div>
      <h1>Cart</h1>
      <table>
        <thead>
          <tr>
            <th>Robot</th>
            <th class='cost'>Cost</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(robot, index) in cart" :key="index">
            <td>
              {{robot.head.title}}
            </td>
            <td class='cost'>
              {{robot.cost}}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>


<script>
import avaliableParts from '../data/parts';

function getPreviousValidIndex(index, length) {
  const daprecateIndex = index - 1;
  return daprecateIndex < 0 ? length - 1 : daprecateIndex;
}

function getNextValidIndex(index, length) {
  const incrementIndex = index + 1;
  return incrementIndex > length - 1 ? 0 : incrementIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      avaliableParts,
      cart: [],
      selectedHeadIndex: 0,
      selectedLeftIndex: 0,
      selectedArmsRightIndex: 0,
      selectedTorsoIndex: 0,
      selectedBasesIndex: 0,
    };
  },
  computed: {
    saleBorderCLass() {
      return this.selectedRobot.head.onSale ? 'sale-border' : '';
    },
    headBorderStyle() {
      return {
        border: this.selectedRobot.head.onSale ? '3px solid blue' : 'none',
      };
    },
    selectedRobot() {
      return {
        head: avaliableParts.heads[this.selectedHeadIndex],
        leftArm: avaliableParts.arms[this.selectedLeftIndex],
        rightArm: avaliableParts.arms[this.selectedArmsRightIndex],
        torsos: avaliableParts.torsos[this.selectedTorsoIndex],
        bases: avaliableParts.bases[this.selectedBasesIndex],
      };
    },
  },
  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost
       + robot.leftArm.cost
       + robot.rightArm.cost
       + robot.torsos.cost
       + robot.bases.cost;
      this.cart.push(Object.assign({}, robot, { cost }));
      console.log(cost);
    },
    selectNextHead() {
      this.selectedHeadIndex = getNextValidIndex(
        this.selectedHeadIndex,
        avaliableParts.heads.length,
      );
    },
    selectPreviousHead() {
      this.selectedHeadIndex = getPreviousValidIndex(
        this.selectedHeadIndex,
        avaliableParts.heads.length,
      );
    },
    selectPreviousLeftArm() {
      this.selectedLeftIndex = getPreviousValidIndex(
        this.selectedLeftIndex,
        avaliableParts.arms.length,
      );
    },
    selectNextLeftArm() {
      this.selectedLeftIndex = getNextValidIndex(
        this.selectedLeftIndex,
        avaliableParts.arms.length,
      );
    },
    selectPreviousRightArm() {
      this.selectedArmsRightIndex = getPreviousValidIndex(
        this.selectedArmsRightIndex,
        avaliableParts.arms.length,
      );
    },
    selectNextRightArm() {
      this.selectedArmsRightIndex = getNextValidIndex(
        this.selectedArmsRightIndex,
        avaliableParts.arms.length,
      );
    },
    selectTorsoPrevious() {
      this.selectedTorsoIndex = getPreviousValidIndex(
        this.selectedTorsoIndex,
        avaliableParts.torsos.length,
      );
    },
    selectTorsoNext() {
      this.selectedTorsoIndex = getNextValidIndex(
        this.selectedTorsoIndex,
        avaliableParts.torsos.length,
      );
    },
    selectBasesPrevious() {
      this.selectedBasesIndex = getPreviousValidIndex(
        this.selectedBasesIndex,
        avaliableParts.bases.length,
      );
    },
    selectBasesNext() {
      this.selectedBasesIndex = getNextValidIndex(
        this.selectedBasesIndex,
        avaliableParts.bases.length,
      );
    },
  },
};
</script>


 <style lang='scss' scoped>
.part {
  position: relative;
  width: 165px;
  height: 165px;
  border: 3px solid #aaa;

}
.part {
  img{
    width: 165px;
  }
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
.head {
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
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index: 1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector,
.center .next-selector {
  opacity: 0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;
  width: 144px;
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
.content {
  position: relative;
}
.add-to-cart {
  position: absolute;
  width: 220px;
  height: 30px;
  padding: 3px;
  font-size: 16px;
}

td, th {
  text-align: left;
  padding: 5px;
  padding-right: 5px;
}
.cost {
  text-align: right;
}
.sale-border{
  border: 3px solid red;
}
</style>
