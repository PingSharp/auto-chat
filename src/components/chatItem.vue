<template>
  <div :class="[chatItemObj.type === 'left'?'left fadeInLeft':'right fadeInRight']" class="animated">
    <img class="avater" :src="[chatItemObj.type === 'left'?require('../assets/left.png'):require('../assets/right.png')]" alt="profie picture">
    <p class="msg">{{chatItemObj.msg}}</p>
  </div>
</template>
<script>
export default {
  props: {
    chatItemObj: {
      type: Object,
      required: true,
      default: {}
    }
  }
}
</script>
<style>
  .avater {
    width: 10%;
  }
  .msg {
    font-size: 1.1em;
    display: inline-flex;
    width: 80%;
    position: absolute;
    left: 15%;
  }
  .right img {
    position: relative;
    left: 90%;
  }
  .right .msg {
    position: absolute;
    left: 5px;
  }
</style>
