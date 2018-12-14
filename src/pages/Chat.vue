<template>

  <div>

    <div class="navbar">

      <span class="navbar-text">{{title}}</span>

    </div>

 <div class="content">

      <div>

        <ul class="message-content" ref="messageContent">

          <li v-for="(item, index) in showMsgDatas" :key="index">
              {{item.msg}}
          </li>

        </ul>

      </div>

    </div>

  </div>

</template>

<script>
  export default {
    data: function () {
      return {
        title: "hi",
        chatDatas: [],
        showMsgDatas: [],
      }
    },
    created: function() {
      this.loadChatData();
    },
    methods: {
      loadChatData: function(){
        var $this = this;
        console.log($this);
        this.$http.get('../../static/chatData.json')
        .then(function(res) {
          console.log(res.data.msgData)
          $this.chatDatas=res.data.msgData;
          $this.setMsg('001');
        });
      },
      setMsg: function (selectId) {
        this.selectMsgData = this.chatDatas.filter((item)=>{
          return item.id === selectId;
        })[0];
        this.setShowMsgDatas(this.selectMsgData.leftMsg,'left');
        this.rightDatas = this.selectMsgData.rightData;
      },

      setShowMsgDatas: function (msgData,type) {
        var $this = this;
        var i = 0;
        if ('left' === type) {
          $this.title = 'Ping is typing...';
          $this.inputDisable = true;
          var interval = setInterval(function(){
            $this.showMsgDatas.push({
              id: $this.selectMsgData.id,
              msg: msgData[i],
              type: type
            });
            // $this.scrollContent();
            i++;
            if(i>= msgData.length) {
              $this.title = 'chatting with Ping';
              $this.inputDisable = false;
              window.clearInterval(interval);
              return;
            }
          },2000);
        } else{
          this.showMsgDatas.push({
            id: $this.selectMsgData.id,
            msg: msgData[0],
            type: type
          });
        }
      }
    }
  }
</script>
<style>
  .navbar-text {
    font-size: 1.5em;
    margin: 35%;
    font-family: sans-serif;
    color: darkblue;
    border: aqua;
    border-style: ridge;
    padding: 5px;
    border-width: medium;
    position: relative;
    top: 20px;
  }
  .message-content li{
    font-size: 1em;
    position: relative;
    top: 50px;
    border: aqua;
    border-style: ridge;
    font-family: cursive;}
</style>
