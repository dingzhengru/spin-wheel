<template>
<div id="spin-wheel">
  <div class="wheel-wrapper">
    <div class="wheel-pointer" @click="onClickRotate">
      Start
    </div>
    <div class="wheel-bg" 
      :class="{freeze: freeze}" 
      :style="{ 'transform': `rotate(${wheelDeg}deg)`,
                'transition': `transform ${time}s ease-in-out`,
                'background': wheelBackground}"
    >
      <div class="prize-list">
        <div class="prize-item-wrapper" v-for="(item,index) in prizeList" :key="index">
          <div class="prize-item" :style="`transform: rotate(${(360 / prizeList.length) * index}deg)`">
            <div class="prize-name">
              {{ item.name }}
            </div>
            <div class="prize-icon">
              <img :src="item.icon">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>

export default {
  name: 'SpinWheel',
  props: {
    prizeList: {
      type: Array,
      default: () => []
    },
    time: { // 旋轉時間
      type: Number,
      default: 4
    },
    wheelBackground: {
      type: String,
      default: () => 'url(https://cdn.clipart.email/7169421ce2382b291dd69957c1f89dcf_free-black-circle-transparent-download-free-clip-art-free-clip-_900-600.jpeg) no-repeat center center'
    }
  },
  data() {
    return {
      freeze: false,
      rolling: false,
      wheelDeg: 0,
    }
  },
  computed: {
    // prizeList() {
    //   return this.prizeList.slice(0, this.prizeNumber)
    // }
  },
  methods: {
    onClickRotate() {
      if (this.rolling) {
        return
      }

      // result: 假設有 8 個獎項 => 0 ~ 8
      // 0~1 代表中第一個 1~2 代表中第二個...以此類推
      const result = Math.floor(Math.random() * this.prizeList.length)
      this.roll(result)
    },
    roll(result) {
      this.rolling = true

      const { wheelDeg, prizeList } = this

      this.wheelDeg =
        wheelDeg -
        wheelDeg % 360 +
        (6 + this.time) * 360 +
        (360 - 360 / prizeList.length * result)

      setTimeout(() => {
        this.rolling = false
        alert("Result：" + prizeList[result].name)
      }, this.time * 1000 + 500)
    }
  },
  // watch: {
  //   prizeNumber() {
  //     this.freeze = true
  //     this.wheelDeg = 0

  //     setTimeout(() => {
  //       this.freeze = false
  //     }, 0)
  //   }
  // }
}
</script>

<style lang="scss">


$wheelWidth: 325px;
$wheelHeight: 325px;

$prizeWidth: $wheelWidth / 2;
$prizeHeight: $wheelHeight / 2;

.wheel-wrapper {
  width: $wheelWidth;
  height: $wheelHeight;

  margin: 0 auto;

  position: relative;
  // position: absolute;
  // top: 50%;
  // left: 50%;
  // transform: translate(-50%, -50%);
}

.wheel-pointer {
  width: 60px;
  height: 60px;
  border-radius: 1000px;

  background: yellow;

  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  line-height: 60px;
  z-index: 10;
  cursor: pointer;

  &::after {
    content: "";
    position: absolute;
    top: -32px;
    left: 50%;
    border-width: 0 8px 40px;
    border-style: solid;
    border-color: transparent transparent yellow;
    transform: translateX(-50%);
  }
}
.wheel-bg {
  width: 100%;
  height: 100%;
  border-radius: 1000px;
  overflow: hidden;
  // transition: transform $transitionTime ease-in-out;

  // background: #7eef97;

  &.freeze {
    transition: none;
    background: red;
  }
}

.prize-list {
  width: 100%;
  height: 100%;
  position: relative;
  text-align: center;
}

.prize-item-wrapper {
  width: $prizeWidth;
  height: $prizeHeight;
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
}

.prize-item {
  width: 100%;
  height: 100%;
  transform-origin: bottom;

  .prize-name {
    padding: 16px 0;
  }

  .prize-icon {
  }
}
</style>
