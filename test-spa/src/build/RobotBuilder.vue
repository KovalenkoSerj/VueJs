<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <img v-bind:src="avaliableParts.heads[selectedHeadIndex].src" title="head"/>
        <button v-on:click="selectPreviousHead()" class="prev-selector">&#9668;</button>
        <button v-on:click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img v-bind:src="avaliableParts.arms[selectedLeftIndex].src" title="left arm"/>
        <button v-on:click="selectPreviousLeftArm()" class="prev-selector">&#9650;</button>
        <button v-on:click="selectNextLeftArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img v-bind:src="avaliableParts.torsos[selectedTorsosIndex].src" title="left arm"/>
        <button v-on:click="selectTorsosPrevious()" class="prev-selector">&#9668;</button>
        <button v-on:click="selectTorsosNext()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img v-bind:src="avaliableParts.arms[selectedArmsRightIndex].src" title="left arm"/>
        <button v-on:click="selectPreviousRightArm()" class="prev-selector">&#9650;</button>
        <button v-on:click="selectNextRightArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img v-bind:src="avaliableParts.bases[selectedBasesIndex].src" title="left arm"/>
        <button v-on:click="selectBasesPrevious()" class="prev-selector">&#9650;</button>
        <button v-on:click="selectBasesNext()" class="next-selector">&#9660;</button>
      </div>
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
      selectedHeadIndex: 0,
      selectedLeftIndex: 0,
      selectedArmsRightIndex: 0,
      selectedTorsosIndex: 0,
      selectedBasesIndex: 0
    };
  },
  methods: {
    selectNextHead() {
      this.selectedHeadIndex = getNextValidIndex(this.selectedHeadIndex, avaliableParts.heads.length);
    },
    selectPreviousHead() {
      this.selectedHeadIndex = getPreviousValidIndex(this.selectedHeadIndex, avaliableParts.heads.length);
    },
    selectPreviousLeftArm() {
      this.selectedLeftIndex = getPreviousValidIndex(this.selectedLeftIndex, avaliableParts.arms.length);
    },
    selectNextLeftArm() {
      this.selectedLeftIndex = getNextValidIndex(this.selectedLeftIndex, avaliableParts.arms.length);
    },
    selectPreviousRightArm() {
      this.selectedArmsRightIndex = getPreviousValidIndex(this.selectedArmsRightIndex, avaliableParts.arms.length);
    },
    selectNextRightArm() {
      this.selectedArmsRightIndex = getNextValidIndex(this.selectedArmsRightIndex, avaliableParts.arms.length);
    },
    selectTorsosPrevious() {
      this.selectedTorsosIndex = getPreviousValidIndex(this.selectedTorsosIndex, avaliableParts.torsos.length);
    },
    selectTorsosNext() {
      this.selectedTorsosIndex = getNextValidIndex(this.selectedTorsosIndex, avaliableParts.torsos.length);
    },
    selectBasesPrevious() {
      this.selectedBasesIndex = getPreviousValidIndex(this.selectedBasesIndex, avaliableParts.bases.length);
    },
    selectBasesNext() {
      this.selectedBasesIndex = getNextValidIndex(this.selectedBasesIndex, avaliableParts.bases.length);
    },
  },
};
</script>


 <style>
  .part {
  position: relative;
  width:165px;
  height:165px;
  border: 3px solid #aaa;
}
.part img {
  width:165px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
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
  z-index:1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
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
 </style>
