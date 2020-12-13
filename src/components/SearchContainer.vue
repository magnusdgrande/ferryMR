<template>
  <div class="search-container">
    <button class="search-button"><font-awesome-icon icon="search" /></button>
    <div class="input-container">
      <input class="input" id="from" v-model="from" />
      <input class="input" id="to" v-model="to" />
    </div>
    <button class="search-button"><font-awesome-icon icon="search" /></button>
  </div>
</template>

<script>
export default {
  name: "SearchContainer",
  props: {},
  data() {
    return {};
  },
  methods: {},
};
</script>
<style lang="scss" scoped>
.search-container {
  display: flex;
  width: calc(100% - 24px);
  margin: 12px;
  .actions-container {
    width: 10%;
  }
  .input-container {
    display: flex;
    flex-direction: column;
    width: 80%;
    .input {
      height: 32px;
      border-radius: 6px;
      margin: 4px;
    }
  }
  .search-button {
    width: 10%;
    height: 84px;
    margin: 4px;
    background: transparent;
    border: none;
    color: white;
    font-size: 22px;
  }
}
</style>