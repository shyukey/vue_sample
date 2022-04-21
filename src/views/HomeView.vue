<template>
  <div class="home">
    <h1>トップページ</h1>
    <div>
      <SearchArea v-model="form" @child-click="BtnClicked(hello)" />
      <GridArea />
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
      someText1: '',
      someText2: '',
    },
  }),
  methods: {
    BtnClicked(v) {
      alert(v);
    }
  }
}
</script>
