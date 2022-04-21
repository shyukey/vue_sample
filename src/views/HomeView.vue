<template>
  <div class="home">
    <h1>トップページ</h1>
    <div>
      <SearchArea v-model="form" @child_click="parent_click(form)" />
      <GridArea ref="grid_area" v-bind:search_word1="form.someText1" v-bind:search_word2="form.someText2" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import SearchArea from '@/components/SearchArea.vue'
import GridArea from '@/components/GridArea.vue'
export default {
  name: 'HomeView',
  components: {
    SearchArea,
    GridArea
  },
  data:() => ({
    form: {
      text_label1: '名前',
      text_label2: '年齢',
      someText1: '',
      someText2: '',
    },
  }),
  methods: {
    parent_click() {
      console.log('イベント発生：parent_click');
      this.$refs.grid_area.search_click();
    }
  }
}
</script>