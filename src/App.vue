<template>
<div id="app">
  <h1>CSS3 轉盤抽獎</h1>
  <code>來自: https://mirari.cc/2019/06/25/CSS3实现转盘抽奖</code>
  
  <SpinWheel 
    :prizeList="prizeList"
    :time="5"
  />

</div>
</template>

<script>

import SpinWheel from '@/components/SpinWheel'

export default {
  name: 'App',
  components: {
    SpinWheel
  },
  data() {
    return {
      prizeList: [
        {
          icon: "https://picsum.photos/40?random=1",
          name: "$10000"
        },
        {
          icon: "https://picsum.photos/40?random=6",
          name: "Thank you!"
        },
        {
          icon: "https://picsum.photos/40?random=2",
          name: "$500"
        },
        {
          icon: "https://picsum.photos/40?random=3",
          name: "$100"
        },
        {
          icon: "https://picsum.photos/40?random=6",
          name: "Thank you!"
        },
        {
          icon: "https://picsum.photos/40?random=4",
          name: "$50"
        },
        {
          icon: "https://picsum.photos/40?random=5",
          name: "$10"
        },
        {
          icon: "https://picsum.photos/40?random=6",
          name: "Thank you!"
        },
      ]
    }
  },
}
</script>

<style lang="scss">

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 20px;
}
</style>
