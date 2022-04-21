<template>
  <div>
    <label>test</label>
  </div>
</template>

<script>

export default {
  name: "BaseGridComponent",
  components: {
  },
  props: {},
  data() {
    return {
      cols: ["Make", "Model", "Year", "Color"],
      rows: [
        ["Ford", "Fusion", "2011", "Silver"],
        ["Chevrolet", "Cruz", "2018", "White"],
      ],
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
