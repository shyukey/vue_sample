<template>
  <div class="form-group">
    <div class="row input-area">
      <label class="label">カスタム入力エリア１</label>
      <input class="form-control" v-model="someText1" />
    </div>
    <div class="row input-area">
      <label class="label">カスタム入力エリア２</label>
      <input class="form-control" v-model="someText2" />
    </div>
    <div class="row">
      <!-- @clickはv-on:clickの省略 -->
      <button @click="child_click_event" class="btn btn-primary">検索</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "SearchArea",
  props: {
    value: {
      type: Object,
      default: () => ({
        someText1: "",
        someText2: "",
      }),
    },
  },
  computed: {
    someText1: {
      get() {
        return this.value.someText1;
      },
      set(v) {
        const that = this.value;
        that.someText1 = v;
        this.$emit("input", that);
      },
    },
    someText2: {
      get() {
        return this.value.someText2;
      },
      set(v) {
        const that = this.value;
        that.someText2 = v;
        this.$emit("input", that);
      },
    },
  },
  methods: {
    child_click_event: function() {
      // 子要素でのクリック処理
      console.log('子要素のクリックイベント');
      // 親に伝播
      this.$emit('child-click');
    }
  }
};
</script>

<style scoped>
.label {
  margin-right: 10px;
}
.input-area {
  margin-bottom: 10px;
}

</style>