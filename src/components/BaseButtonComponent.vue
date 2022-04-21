<template>
  <div class="container">
    <div class="row">
      <a>1.親コンポーネントの伝播</a>
    </div>
    <div class="row">
      <input type="text" v-model="search_text" />
      <button class="btn btn-primary" v-on:click="button1_click">
        Button1
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderComponent",
  components: {},
  props: {},
  data() {
    return {
      search_text: "test",
    };
  },
  methods: {
    button1_click: function () {
      alert("子コンポーネント押下イベント");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
nav {
  padding: 30px;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
}
nav a.router-link-exact-active {
  color: #42b983;
}
</style>