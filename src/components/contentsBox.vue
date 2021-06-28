<template>
  <div class="sec-mb">
    <contentsItem
      v-for="item in sec"
      :key="item.id"
      :contents="item"
      :name="name"
    ></contentsItem>
  </div>
</template>

<script>
import contentsItem from "./contentsItem.vue";
import { getData, getTypes, sleep } from "../services/index.js";
import { down } from "../services/index.js";

export default {
  components: {
    contentsItem,
  },
  props: {
    tag: Number,
  },
  data() {
    return {
      sec: [],
      page: 0,
      name: "",
    };
  },
  methods: {
    async getDataFn() {
      //????去掉1、2行
      // let res = await getData(this.tag, this.page); // 200ms
      // let types = await getTypes(); // 200ms

      await sleep(1000); //防止typesBox与contentsBox同时请求同一个函数getTypes()

      let ps = await Promise.all([getData(this.tag, this.page), getTypes()]);
      console.log(123, ps);

      let [res, types] = ps;

      this.sec = this.sec.concat(res);

      types.map((item) => {
        item.tag == this.tag ? (this.name = item.name) : false;
      }); //需在data中定义name属性值

      // getData()(
      //   (res) => {
      //     this.sec = this.sec.concat(res);
      //   },
    },
  },
  created() {
    //   let res = await getData();
    // this.sec = res;

    this.getDataFn();

    down(() => {
      //不能用期约的方式做，因为回调函数会多次使用
      this.page++;
      this.getDataFn(this.getDataFn());
    });

    // let res = await getTypes(res.data[0].tag); //以期约方式提取types.tag的尝试
    // console.log(res);
  },
  watch: {
    tag: function (a, b) {
      console.log(111, this.tag);
      this.sec = [];
      this.page = 0;
      this.getDataFn();
    },
  },
};
</script>

<style>
.sec-mb {
  padding-bottom: 50px;
}
</style>