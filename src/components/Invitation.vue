<template>
  <div class="wedding-invitation" :class="{ 'invitation-bounce':canOpen }">
    <div class="invitation-container" :class="{ 'invitation-down':isOpening }">
      <div class="invitation-cover">
        <div class="cover-content" :class="{'invitation-up':isOpening}">
          <div class="content-inside">
            <img class="content-inside-photo" src="https://cdn.jsdelivr.net/gh/luckyu2/imgLibrary@main/ruiqiImg/_63A1727_1.webp">
            <p>我们结婚啦！</p>
            <p><b>余司胜 & 罗瑞琪</b></p>
            <p>时间：2022年2月6日</p>
            <p>地点：<b>应城市XX酒店</b></p>
            <div class="content-inside-bless">
              <input
                placeholder="在此，写下你的祝福吧"
                @keyup.enter="sendBarrage"
                @focus="isFocused = true"
                @blur="isFocused = false, hasEntered = false"
                v-model="wish"
                ref="wishInput"
              >
              <p v-if="!wish && isFocused && hasEntered">请输入祝福哦</p>
              <div>
                <button @click="sendBarrage">发送祝福 &nbsp  💌</button>
                <button @click="closeInvitation">关闭</button>
              </div>
            </div>
            <div class="content-inside-about">
              <a @click="$router.push({ path: '/she' })">
                <img src="../assets/images/nv.png" alt="女">
                <p style="color: palevioletred"> 关于她</p>
              </a>

              <a @click="$router.push({ path: '/man' })">
                <img src="../assets/images/nan.png" alt="nan">
                <p> 关于他</p>
              </a>
            </div>
          </div>
        </div>
        <div class="cover-inside-left" :class="{'opening':isOpening}">
          <img style="height: 30vh;margin:15vh 10vh " src="../assets/images/yq.png" alt="邀请函">
        </div>
        <div class="cover-inside-right" :class="{'opening':isOpening}"></div>
        <img class="cover-inside-seal" src="../assets/images/seal.png" @click="openInvitation" :class="{'invitation-flight':isOpening}">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['canOpen'],
  data() {
    return {
      isOpening: false,
      wish: '',
      isFocused: false,
      hasEntered: false
    }
  },
  methods: {
    // 打开邀请函
    openInvitation(){
      this.isOpening = true
    },
    closeInvitation () {
      this.isOpening = false
      setTimeout(() => {
        this.$emit('onClose')
      }, 660)
    },
    // 发送弹幕
    sendBarrage(){
      this.$nextTick(() => {
        this.hasEntered = true
        if (!this.wish) {
          return
        }
        this.isOpening = false
        this.$refs.wishInput.blur()
        setTimeout(() => {
          this.$emit('sendBarrage', this.wish)
        }, 660)
      })
    }
  }
}
</script>

<style lang="less">
  .wedding-invitation{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    padding: 0 20px;
    padding-top: 60px;
    z-index: 4;
    transform: scale(0.05);
    -webkit-transform: scale(0.05);
    opacity: 0;
    transition: transform 0.8s cubic-bezier(.26,1.84,.39,.61), opacity 0.5s linear;
    -webkit-transition: -webkit-transform 0.8s cubic-bezier(.26,1.84,.39,.61), opacity 0.5s linear;
    background-size: 100%;
    overflow: hidden;
    &.invitation-bounce{
      opacity: 1;
      transform: scale(1);
      -webkit-transform: scale(1);
    }
    .invitation-container{
      position: relative;
      width: 100%;
      height: 100%;
      transition: transform 0.6s cubic-bezier(0.4, 0, 1, 1);
      -webkit-transition: -webkit-transform 0.6s cubic-bezier(0.4, 0, 1, 1);
      &.invitation-down{
        transform: translateY(20px);
        -webkit-transform: translateY(20px);
      }
      .invitation-cover{
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: #D65047;
        border-radius: 10px;
        perspective: 500px;
        box-shadow: 0 0 20px 2px rgba(0, 0, 0, 0.15);
        .cover-content{
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          padding: 10px 20px;
          transition: transform 0.6s cubic-bezier(0.4, 0, 1, 1);
          -webkit-transition: -webkit-transform 0.6s cubic-bezier(0.4, 0, 1, 1);
          &.invitation-up{
            transform: translateY(-60px);
            -webkit-transform: translateY(-60px);
          }
          .content-inside{
            height: 94vh;
            padding: 20px;
            color: #a9895d;
            background-color: #FFF1DE;
            text-align: center;
            overflow: auto;
            &-photo{
              height: 50vh;
              /*width: 100%;*/
              margin-bottom: 10px;
              padding: 5px;
              border: 1px solid #f7debb;
            }
            p{
              margin-top: 0;
              margin-bottom: 5px;
            }
            &-bless{
              input{
                width: 100%;
                height: 35px;
                margin-bottom: 10px;
                outline: none;
                border: none;
                border-bottom: 1px solid #f7debb;
                /*color: #a9895d;*/
                color: #e78909;
                background: transparent;
                /*background: #F2F2F2;*/
                font-size: 16px;
                &::-webkit-input-placeholder { color: #E8D1B1;font-size: 12px; }
                &::-moz-placeholder { color: #E8D1B1;font-size: 12px; }
                &:-ms-input-placeholder { color: #E8D1B1;font-size: 12px; }
                &:-moz-placeholder { color: #E8D1B1;font-size: 12px; }
              }
              >div{
                display: flex;
                button{
                  width: 100%;
                  height: 35px;
                  color: #a9895d;
                  background: #f7debb;
                  border: none;
                  outline: none;
                  &:disabled{
                    opacity: 0.8;
                  }
                  &:first-child{
                    margin-right: 10px;
                    flex: 1;
                  }
                  &:last-child{
                    width: 60px;
                    border: 1px solid #f7debb;
                    background: transparent;
                  }
                }
              }
            }
            &-about{
              margin-top: 40px;
              display: flex;
              justify-content:space-around;
             a {
               border: 1px solid red;
                width: 50px;
                height: 50px;
                border-radius: 50%;
              }

            }
          }
        }
        .cover-inside-left{
          position: absolute;
          left: 0;
          top: 0;
          width: 70%;
          height: 100%;
          border-radius: 10px;
          background-color: #D65047;
          box-shadow: 5px 0 10px rgba(0,0,0,0.2);
          z-index: 6;
          transition: transform 0.5s;
          -webkit-transition: -webkit-transform 0.5s;
          transform-origin: 0 50%;
          -webkit-transform-origin: 0 50%;
          &.opening{
            transform: rotate3d(0,1,0,-140deg);
            -webkit-transform: rotate3d(0,1,0,-140deg);
          }
        }
        .cover-inside-right{
          position: absolute;
          right: 0;
          top: 0;
          width: 40%;
          height: 100%;
          border-radius: 10px;
          background-color: #D65047;
          box-shadow: -5px 0 10px rgba(0,0,0,0.2);
          z-index: 5;
          transition: transform 0.5s;
          -webkit-transition: -webkit-transform 0.5s;
          transform-origin: 100% 50%;
          -webkit-transform-origin: 100% 50%;
          &.opening{
            transform: rotate3d(0,1,0,140deg);
            -webkit-transform: rotate3d(0,1,0,140deg);
          }
        }
        .cover-inside-seal{
          position: absolute;
          left: 70%;
          bottom: 100px;
          width: 80px;
          height: 80px;
          margin-left: -40px;
          z-index: 7;
          transform-origin: 50% 50%;
          -webkit-transform-origin: 50% 50%;
          transition: all 0.8s cubic-bezier(0.4, 0, 1, 1);
          -webkit-transition: all 0.8s cubic-bezier(0.4, 0, 1, 1);
          &.invitation-flight{
            opacity: 0;
          }
        }
      }
    }
  }
</style>
