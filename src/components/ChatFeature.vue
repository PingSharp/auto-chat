<template>
  <div>
    <div class="chat-footer" @click="onTogglePop()">
            <div class="send-msg">
               Choose your messages...
            </div>

            <div class="send-btn">
              <button>choose</button>
            </div>
    </div>
    <div class="send-msg-pop animated fast" :class="[togglePop ? 'slideInUp' : 'slideOutDown']" >
            <div class="chat-footer">
                <div class="send-msg">
                    Choose your messages...
                </div>

                <div class="send-btn">
                   <button>choose</button>
                </div>
            </div>
            <div class="choose-msg">
                <ul>
                    <li v-for="(item, index) in rightDatas" :key="index" @click="onRightSelectMsg(item)">
                        {{item.rightMsg[0]}}
                    </li>
                </ul>
            </div>
     </div>

  </div>
</template>
<script>
export default {
    props: {
        inputDisable: {
            type: Boolean,
            required: true,
            default: true
        },
        rightDatas: {
            type: Array,
            required: true,
            default: []
        },
    },
    data: function () {
        return {
            togglePop: false,
        }
    },
    methods: {
        onTogglePop: function () {
            if (this.inputDisable) {
                return;
            }
            debugger;
            console.log(this._props.rightDatas);
            this.togglePop = !this.togglePop;
        },
        onRightSelectMsg: function (item) {
            this.$emit('onRightSelectMsg', item);
            this.togglePop = false;
        }
    }
}
</script>
<style>
  div.chat-footer {
    position: absolute;
    top: 81%;
    left: 2%;
    border-style: solid;
    width: 95%;
    height: 15%;
    border-color: aquamarine;
  }
  div.send-btn {
    position: absolute;
    right: 5%;
    top: 110%;
  }
  div.send-btn button {
    background-color: aquamarine;
        padding: 10px;
    font-size: medium;
    font-weight: bold;
    font-family: sans-serif;
  }
 div.send-msg-pop {
   display: none;
 }
 div.choose-msg {
   height: 300px;
   width: 100%;
   position: absolute;
    top: 63%;
    border-style: inset;
    border-color: aquamarine;
        border-bottom: none;
         border-right: none;
         border-left: none;
}
 div.choose-msg ul {
   height: 100%;
   width: 100%;
 }
 div.choose-msg ul li {
   border-bottom-style: inset;
    border-bottom-color: aquamarine;
 }
 div.slideInUp {
   display: block;
 }
</style>
