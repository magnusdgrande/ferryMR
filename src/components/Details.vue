<template>
  <div class="details">
    <div class="top-container">top</div>
    <div class="bottom-container">bottom</div>
  </div>
</template>

<script>
export default {
  name: "Details",
  props: {
    selectedRoute: { type: Object, default: () => {} },
  },
  data() {
    return {};
  },
  methods: {},
};
</script>
<style lang="scss" scoped>
.details {
  height: calc(100vh - 84px);
  overflow: auto;
  background: white;
  color: black;
  .top-container {
    height: 15%;
  }
  .bottom-container {
    height: 85%;
  }
}
</style>