<template>
  <div class="row">
    <grid :cols="cols" :rows="rows"></grid>
  </div>
</template>

<script>
import Grid from 'gridjs-vue'
export default {
  name: "SearchArea",
  components: {
    Grid,
  },
  props: {
    value: {
      type: Object,
      default: () => ({
        someText1: "",
        someText2: "",
      }),
    },
  },
  methods: {
    child_click_event: function () {
      // 子要素でのクリック処理
      console.log("子要素のクリックイベント");
      // 親に伝播
      this.$emit("child-click");
    },
  },
};
</script>

<style scoped>
.label {
  margin-right: 10px;
}
.input-area {
  margin-bottom: 10px;
}
.search-button-area {
  float: right;
}
</style>