<template>
  <div id="app">
    <header class="header-box">
      <h5 class="head">行情资讯</h5>
    </header>
    <typesBox @tapChange="tapChange"></typesBox>
    <contentsBox :name="currentName" :tag="currentTag"></contentsBox>
  </div>
</template>

<script>
import typesBox from "./components/typesBox.vue";
import contentsBox from "./components/contentsBox.vue";

export default {
  components: {
    typesBox,
    contentsBox,
  },
  data() {
    //设置属性值的初始值
    return {
      currentName: "报价",
      currentTag: 1,
    };
  },
  methods: {
    tapChange(name, tag) {
      this.currentName = name;
      this.currentTag = tag;
    },
  },
};
</script>

<style>
#app {
  background-color: #f8f8f8;
  font-size: 14px;
}
.header-box {
  padding-top: 30px;
  background-color: rgba(248, 248, 248, 0.82);
  border-bottom: 1px solid #b9b9b9;
}
.head {
  line-height: 33px;
  text-align: center;
  font-size: 17px;
  font-family: Helvetica;
  font-weight: 400;
}
</style>
