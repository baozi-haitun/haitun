<template>
  <li class="nav" @click="click" :class="{ active: active }">
    {{ name }}
  </li>
</template>

<script>
export default {
  props: {
    content: Object,
    active: Boolean, //item.active
  },
  data() {
    return {
      name: "",
      tag: null,
    };
  },
  created() {
    let { name, tag } = this.content;
    this.name = name;
    this.tag = tag;
  },
  methods: {
    click() {
      this.$emit("tap", this.name, this.tag);
    },
  },
};
</script>

<style>
.nav {
  margin-top: 8px;
  margin-left: 15px;
  float: left;
  width: 55px;
  height: 26px;
  background-color: #ffffff;
  line-height: 26px;
  text-align: center;
  border: 1px solid #eeeeee;
  border-radius: 4px;
}
.nav.active {
  border: 1px solid #19ad18;
  color: #19ad18;
  background-color: rgba(25, 173, 24, 0.2);
}
</style>