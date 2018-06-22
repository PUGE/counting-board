<template>
  <div class="board">
    <div v-for="(item, ind) in String(num)" class="clock" :key="ind">
      <div class="clock__number-wrapper" :class="{clock__number_wrapper_open: isOpen}" :key="ind">
        <span class="clock__section clock__section--next">
          <span class="clock__number js-increment-after">{{item}}</span>
        </span>
        <span class="clock__section clock__section--upper">
          <span class="clock__number js-increment-before">{{String(oldNum)[ind]}}</span>
        </span>
        <span class="clock__section clock__section--upper-back">
          <span class="clock__number js-increment-after">{{item}}</span>
        </span>
        <span class="clock__section clock__section--lower">
          <span class="clock__number js-increment-before">{{String(oldNum)[ind]}}</span>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    num: Number
  },
  data () {
    return {
      oldNum: 0,
      isOpen: false
    }
  },
  created () {
    // 初始化完成后就显示一次数值
    this.oldNum = this.num
  },
  watch: {
    num (newNum, old) {
      console.log(newNum, old)
      this.isOpen = true
      setTimeout(() => {
        this.oldNum = this.num
        this.isOpen = false
      }, 500)
    }
  }
}
</script>

<style scoped>
.board {
  display: flex;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
  height: 110px;
  justify-content: center;
}
.clock {
  width: 80px;
  height: 100px;
  margin: 10px;
  font-family: Arial;
  line-height: 1;
  perspective: 400px;
}
.clock__section {
  display: block;
  background-color: #333;
  color: #fff;
  position: absolute;
  left: 0;
  font-size: 100px;
  width: 80px;
  height: 49px;
  overflow: hidden;
  backface-visibility: hidden;
}

.clock__section--lower:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 80px;
  height: 49px;
  opacity: 0;
  background-color: rgba(0, 0, 0, 0.75);
  transition: none;
}
.clock__number_wrapper_open .clock__section--lower:after {
  transition: opacity 0.5s;
  opacity: 1;
}

.clock__section--next {
  top: 0;
  z-index: 1;
  transform-origin: 50% 100%;
}

.clock__section--upper {
  top: 0;
  z-index: 1;
  transform-origin: 50% 100%;
  transition: none;
}
.clock__number_wrapper_open .clock__section--upper {
  transition: transform 0.5s;
  transform: rotateX(-180deg);
}

.clock__section--upper-back {
  top: 0;
  z-index: 7;
  transform-origin: 50% 50px;
  transition: none;
  transform: rotateY(180deg) rotateX(-360deg);
}
.clock__number_wrapper_open .clock__section--upper-back {
  transition: transform 0.5s;
  transform: rotateY(180deg) rotateX(-180deg);
}

.clock__section--lower {
  margin-top: -40px;
  bottom: 0;
}

.clock__number {
  position: absolute;
  text-align: center;
  width: 80px;
}
.clock__section--lower .clock__number {
  bottom: 0;
}
.clock__section--upper-back .clock__number {
  bottom: 0;
  transform: rotateZ(180deg) translateY(-52px);
}
</style>
