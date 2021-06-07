<template>
  <div class="w_scroll-shel" >
    <h1>无缝滚动效果(使用此功能, 更希望大家做成组件; 其中好处那是大大滴有)</h1>
    <scroll class="w_scroll-outer" :data="listData" :class-option="defaultOption" @click="getDetailCont($event)">
      <ul class="w_scro-cont-outer">
        <li
        class="w_scro-item"
        v-for="(item, index) in listData"
        :key="index">
          <h4>{{ item }}</h4>
          <p>{{ item }} -- kkkkkkkkkk</p>
          <p class="w_btn-detail" :id="item">点击查看弹框详情</p>
        </li>
      </ul>
    </scroll>
  </div>
</template>

<script>
import scroll from 'vue-seamless-scroll/src'
import axios from 'axios'

export default {
  name: 'About',
  components: {
    scroll
  },
  data() {
    return {
      checkBtn: 'checkBtn',
      listData: [
        // {
        //   title: '安会计刚发的',
        //   date: '2021/06/01-15:38',
        //   id: 1,
        // },
        // {
        //   title: '安会计刚发的',
        //   date: '2021/06/01-15:38',
        //   id: 2,
        // },
        // {
        //   title: '安会计刚发的',
        //   date: '2021/06/01-15:38',
        //   id: 4,
        // },
        // {
        //   title: '安会计刚发的',
        //   date: '2021/06/01-15:38',
        //   id: 8,
        // },
        // {
        //   title: '安会计刚发的',
        //   date: '2021/06/01-15:38',
        //   id: 12,
        // }
      ],
    }
  },
  computed: {
    defaultOption() {
      return {
        step: 2,          // 数值越大速度滚动越快
        limitMoveNum: 5,  // 开始无缝滚动的数据量 this.dataList.length
        hoverStop: true,  // 是否开启鼠标悬停stop
        direction: 1,     // 0向下 1向上 2向左 3向右
        openWatch: true,  // 开启数据实时监控刷新dom
        singleHeight: 0,  // 单步运动停止的高度(默认值0是无缝不停止的滚动) direction => 0/1
        singleWidth: 0,   // 单步运动停止的宽度(默认值0是无缝不停止的滚动) direction => 2/3
        waitTime: 1000    // 单步运动停止的时间(默认值1000ms)
      }
    }
  },
  mounted() {
    this.getJavaData()
  },
  created() {},
  methods: {
    // btn 按钮的操作事件 (对一些点击弹出详情弹框; 或者获取相关数据, 可以在这里进行操作)
    getDetailCont(e) {
      console.log(e.target.id);
      if(e.target.id !== '' && e.target.id !== null && e.target.id !== undefined) {
        alert(e.target.id)
      }
    },
    // 新搭建 vue 环境, 对 axios 没有封装, 直接使用原生方法, 获取数据 。
    getJavaData() {
      const _this = this
      axios.get('http://125.124.67.201/v1/api/GovBigScreenController/deviceWorkRate?day=1&device=全部&industry=全部&region=全部')
      .then(function (response) {
        _this.listData = response.data.body.date
        console.log("this.listData : ", this.listData);
      })
      .catch(function (error) {
        console.log(error);
      });
    }
  },
}
</script>

<style lang="scss">
.w_scroll-shel {
  .w_scroll-outer {
    background-color: skyblue;
    height: 200px;
    width: 800px;
    overflow: hidden;
  }
  .w_scro-cont-outer {
    margin: 0;
  }
  .w_scro-item {
    background-color: steelblue;
    display: flex;
    justify-content: space-around;
  }
  .w_btn-detail {
    cursor: pointer;
    background-color: tan;
    height: 100%;
  }
}
</style>

