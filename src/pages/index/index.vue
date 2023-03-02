<template>
  <view class="index">
    <view class="header">
      <text>早上好！{{ userName }}</text>
      <view class="header-r">
        <text class="iconfont">&#xe759;</text>
        <text class="header-r-tip">{{ hint }}</text>
      </view>
    </view>
    <nut-swiper class="banner" :loop="true" @change="change">
      <nut-swiper-item>
        <img
          src="https://storage.360buyimg.com/jdc-article/NutUItaro34.jpg"
          alt=""
        />
      </nut-swiper-item>
      <nut-swiper-item>
        <img
          src="https://storage.360buyimg.com/jdc-article/NutUItaro2.jpg"
          alt=""
        />
      </nut-swiper-item>
      <nut-swiper-item>
        <img
          src="https://storage.360buyimg.com/jdc-article/welcomenutui.jpg"
          alt=""
        />
      </nut-swiper-item>
      <nut-swiper-item>
        <img
          src="https://storage.360buyimg.com/jdc-article/fristfabu.jpg"
          alt=""
        />
      </nut-swiper-item>
      <!-- <template v-slot:page>
          <div class="page">{{ current }}/4</div>
        </template> -->
    </nut-swiper>
    <view class="menu">
      <view class="memu-item" v-for="(item, index) in menuList" :key="index">
        <img :src="item.src" alt="" />
        <text>{{ item.name }}</text>
      </view>
    </view>
    <view class="container">
      <view
        class="container-item"
        v-for="(item, index) in actionList"
        @click="showPop($event, index)"
        :key="index"
      >
        <img :src="item.src" alt="" />
        <text class="container-item-txt">{{ item.name }}</text>
      </view>
    </view>
    <view class="footer">
      <view class="footer-item" v-for="(nav, index) in navList" :key="index">
        <template v-if="nav.src">
          <img :src="actionIndex === index ? nav.srcA : nav.src" alt="" />
          <text :style="{ color: actionIndex === index ? '#1afa29' : '' }">{{
            nav.name
          }}</text>
        </template>
        <view v-else class="circle">
          <view class="circle-a"></view>
          <text class="footer-item-txt">常用</text>
          <view class="footer-add">
            <view class="footer-add-bor"></view>
            <view class="footer-add-bg"></view>
            <img :src="require('../../assets/b-a.png')" alt="" />
          </view>
        </view>
      </view>
    </view>
    <Transition name="fade">
      <view class="pop" v-show="isShow" @click="isShow = false">
        <view class="pop-zoom" :style="{ '--x': x, '--y': y }">
          <view class="pop-box" @click.stop="isShow = true">
            <view class="pop-head">{{ action2Name }}</view>
            <view class="pop-box-ct">
              <view
                class="pop-box-ct-item"
                v-for="(item, index) in action2List"
                :key="index"
              >
                <img :src="item.src" alt="" />
                <text>{{ item.name }}</text>
              </view>
            </view>
          </view>
        </view>
      </view>
    </Transition>
  </view>
</template>

<script>
import { Dongdong } from '@nutui/icons-vue-taro'
import { toRefs, ref, reactive, onMounted } from 'vue'
import Taro from '@tarojs/taro'
export default {
  name: 'Index',
  components: {
    Dongdong,
  },
  setup() {
    const state = reactive({
      x: 0,
      y: 0,
      page3: 0,
      current: 1,
      userName: '张三先生',
      hint: 77,
      actionIndex: 0,
      menuList: [
        {
          src: require('../../assets/m1.png'),
          name: '功能1',
        },
        {
          src: require('../../assets/m2.png'),
          name: '功能2',
        },
        {
          src: require('../../assets/m3.png'),
          name: '功能3',
        },
        {
          src: require('../../assets/m4.png'),
          name: '功能4',
        },
        {
          src: require('../../assets/m5.png'),
          name: '功能5',
        },
      ],
      actionList: [
        {
          src: require('../../assets/a1.png'),
          name: '功能1',
        },
        {
          src: require('../../assets/a1.png'),
          name: '功能2',
        },
        {
          src: require('../../assets/a1.png'),
          name: '功能3',
        },
        {
          src: require('../../assets/a1.png'),
          name: '功能4',
        },
        {
          src: require('../../assets/a2.png'),
          name: '功能5',
        },
        {
          src: require('../../assets/a3.png'),
          name: '功能6',
        },
        {
          src: require('../../assets/a4.png'),
          name: '功能7',
        },
        {
          src: require('../../assets/a5.png'),
          name: '功能8',
        },
        {
          src: require('../../assets/a6.png'),
          name: '功能9',
        },
        {
          src: require('../../assets/a7.png'),
          name: '功能10',
        },
      ],
      navList: [
        {
          src: require('../../assets/b1.png'),
          srcA: require('../../assets/b1-a.png'),
          name: '首页',
        },
        {
          src: require('../../assets/b2.png'),
          srcA: require('../../assets/b2-a.png'),
          name: '首页',
        },
        {
          src: '',
        },
        {
          src: require('../../assets/b3.png'),
          srcA: require('../../assets/b3-a.png'),
          name: '首页',
        },
        {
          src: require('../../assets/b4.png'),
          srcA: require('../../assets/b4-a.png'),
          name: '首页',
        },
      ],
      action2List: [
        {
          src: require('../../assets/a1.png'),
          name: '功能1',
        },
        {
          src: require('../../assets/a1.png'),
          name: '功能2',
        },
        {
          src: require('../../assets/a1.png'),
          name: '功能3',
        },
        {
          src: require('../../assets/a1.png'),
          name: '功能4',
        },
        {
          src: require('../../assets/a2.png'),
          name: '功能5',
        },
        {
          src: require('../../assets/a3.png'),
          name: '功能6',
        },
        {
          src: require('../../assets/a4.png'),
          name: '功能7',
        },
        {
          src: require('../../assets/a5.png'),
          name: '功能8',
        },
        {
          src: require('../../assets/a6.png'),
          name: '功能9',
        },
        {
          src: require('../../assets/a7.png'),
          name: '功能10',
        },
      ],
      isShow: false,
      action2Name: '',
    })
    const change = (index) => {
      state.current = index + 1
    }
    function showPop(e, index) {
      console.log(Taro.getEnv())
      if (Taro.getEnv() === 'WEB') {
        let el = e.target
        let { width, height, top, left } = el.getClientRects()[0]
        state.x = width / 2 + left + 'px'
        state.y = height / 2 + top + 'px'
      } else {
        let { x, y } = e.target
        state.x = x + 'px'
        state.y = y + 'px'
      }
      state.action2Name = state.actionList[index].name
      state.isShow = true
    }
    return {
      ...toRefs(state),
      change,
      showPop,
    }
  },
}
</script>
<style lang="scss">
.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s cubic-bezier(0.65, 0.05, 0.36, 1);
  .pop-zoom {
    transition: all 0.3s cubic-bezier(0.65, 0.05, 0.36, 1);
  }
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  .pop-zoom {
    transform-origin: left top;
    left: var(--x) !important;
    top: var(--y) !important;
    transform: scale(0) !important;
  }
}
.index {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: rgb(241, 241, 241);
  min-height: 100vh;
  padding-bottom: 100px;
  .header {
    position: relative;
    background: rgb(29, 42, 59);
    padding: 24px 0;
    font-size: 32px;
    color: rgb(128, 182, 41);
    .header-r {
      position: absolute;
      right: 15px;
      top: 0px;
      display: flex;
      justify-content: center;
      align-items: center;
      top: 50%;
      transform: translate(0%, -50%);
      .iconfont {
        font-size: 54px;
      }
      .header-r-tip {
        position: absolute;
        width: 35px;
        height: 35px;
        border-radius: 50%;
        right: 0;
        top: 0;
        background: rgb(252, 2, 0);
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 24px;
        transform: translate(20%, 20%);
      }
    }
  }
  .banner {
    height: 367px;
    img {
      height: 100%;
      object-fit: cover;
    }
  }
  .menu {
    // height: 106px;
    background: rgb(29, 42, 59);
    display: flex;
    justify-content: space-around;
    padding: 20px 0;
    .memu-item {
      flex: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      color: rgb(134, 137, 152);
      font-size: 16px;
      img {
        width: 50px;
        height: 50px;
        margin-bottom: 10px;
      }
    }
  }
  .container {
    display: flex;
    flex-wrap: wrap;
    background: #fff;
    .container-item {
      width: calc(100vw / 4);
      height: calc(100vw / 4);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      box-shadow: 0px 0px 2px 0px rgba(0, 0, 0, 0.3);
      font-size: 20px;
      .container-item-txt {
        margin-top: 10px;
      }
      img {
        width: 100px;
        height: 100px;
      }
    }
  }

  .footer {
    height: 108px;
    position: fixed;
    bottom: 0px;
    background: #fff;
    left: 0;
    right: 0;
    display: flex;
    font-size: 20px;
    border-top: 1px solid #eeeeee;
    .circle-a {
      width: 40px;
      height: 40px;
      background: #fff;
      border-radius: 50%;
    }
    .footer-item {
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      img {
        width: 40px;
        height: 40px;
        margin-bottom: 5px;
      }
    }
    .footer-item-txt {
      position: relative;
      z-index: 1;
    }
    .footer-add {
      top: 0px;
      position: absolute;
      left: 50%;
      display: flex;
      flex-direction: column;
      display: flex;
      justify-content: center;
      align-items: center;
      transform: translate(-50%, -40%);
      padding: 10px;

      .footer-add-bor {
        position: absolute;
        width: 100%;
        height: 100%;
        border: 1px solid #eeeeee;
        border-radius: 50%;
        background: #fff;
      }
      img {
        width: 85px;
        height: 85px;
        background: #1afa29;
        border-radius: 50%;
        z-index: 1;
      }
      .footer-add-bg {
        position: absolute;
        width: 102%;
        // width: 100%;
        height: 60%;
        bottom: 0px;
        background: #fff;
      }
    }
  }

  .pop {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.7);
    z-index: 999;
    // display: flex;
    // justify-content: center;
    // align-items: center;
    transition: all 0.3s cubic-bezier(0.65, 0.05, 0.36, 1);
    .pop-zoom {
      transform-origin: left top;
      transition: all 0.3s cubic-bezier(0.65, 0.05, 0.36, 1);
      left: 50%;
      top: 50%;
      position: absolute;
      width: 80%;
    }
    .pop-box {
      transform: translate(-50%, -50%);
      background: #fff;
      border-radius: 10px;
      // transform: translate(-50%, -50%);
      // transition: all 0.5s ease;
      .pop-head {
        background: rgb(29, 42, 59);
        border-radius: 10px 10px 0 0;
        padding: 24px 0;
        font-size: 32px;
        display: flex;
        justify-content: center;
        align-items: center;
        color: rgb(111, 142, 29);
      }
      .pop-box-ct {
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        .pop-box-ct-item {
          margin: 20px 0;
          width: calc(100% / 4);
          flex-direction: column;
          font-size: 24px;
          display: flex;
          justify-content: center;
          align-items: center;
          color: rgb(166, 166, 166);
          img {
            width: 80px;
            height: 80px;
            margin-bottom: 15px;
          }
        }
      }
    }
  }
}
</style>
