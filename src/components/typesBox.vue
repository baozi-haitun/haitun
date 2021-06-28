<template>
  <ul class="nav-list">
    <typesItem
      @tap="ontap"
      v-for="item in types"
      :content="item"
      :active="item.active"
      :key="item.tag"
    >
    </typesItem>
  </ul>
</template>

<script>
import { getTypes } from "../services/index.js";
import typesItem from "./typesItem.vue";

export default {
  components: {
    typesItem,
  },

  //data返回值，生命钩子函数
  data() {
    return { types: [] };
  },
  async created() {
    //使用async的函数里面使用await

    // getTypes((res) => {
    //   this.types = res;
    // });

    // let p = getTypes()
    // p.then((res) => {
    //   this.types = res;
    // });

    console.log("typesBox: ");
    let res = await getTypes(); //以期约方式提取types.tag的尝试
    this.types = res;
  },
  methods: {
    ontap(name, tag) {
      var types = this.types.map((abc) => {
        if (abc.tag == tag) {
          abc.active = true;
        } else {
          abc.active = false;
        }
        return abc;
      });
      this.types = types;
      this.$emit("tapChange", name, tag);
    },
  },
};
</script>

<style>
.nav-list {
  height: 72px;
  background-color: rgba(248, 248, 248, 0.82);
}
</style>