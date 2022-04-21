<template>
  <div class="row">
    <vue-good-table :columns="columns" :rows="rows" />
  </div>
</template>

<script>
export default {
  name: "SearchArea",
  components: {},

  props: ["search_word1", "search_word2", "result"],
  methods: {
    search_click: function () {
      console.log("イベント発生：search_click");
      const that = this;
      const all_data = [
        { id: 1, name: "太郎", age: 20, sex: "男性" },
        { id: 2, name: "花子", age: 24, sex: "女性" },
        { id: 3, name: "次郎", age: 16, sex: "男性" },
        { id: 4, name: "トム", age: 20, sex: "男性" },
        { id: 5, name: "メアリー", age: 24, sex: "女性" },
        { id: 6, name: "ボブ", age: 20, sex: "男性" },
        { id: 7, name: "ジョン", age: 24, sex: "女性" },
        { id: 8, name: "万次郎", age: 16, sex: "男性" },
      ];
      this.rows = all_data.filter(function (item) {
        if (that.search_word1 == '' && that.search_word2 == '') return true;
        if (item.age == that.search_word2) {
          return true;
        }
        if (item.name == that.search_word1) {
          return true;
        }
      });
      const test =all_data.filter(function (item) {
        console.log(item.name == that.search_word1);
        if (item.name == that.search_word1) return true;
      });
      console.log(test);
    },
  },
  computed: {},
  data() {
    return {
      columns: [
        { label: "名前", field: "name" },
        { label: "年齢", field: "age", type: "number" },
        { label: "性別", field: "sex" },
      ],
      rows: [],
    };
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