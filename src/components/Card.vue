<template>
  <div class="card">
    <div class="header"></div>
    <div class="content"></div>
    <div class="pie"></div>
  </div>
</template>

<script>
export default {
  name: "Card"
};
</script>

<style scoped lang="scss">
  .card {
    max-width: 35%;
    height: 100px;
    background: $card_bg;
    border-radius: 0.5rem;
    margin: 0 auto;
    box-shadow: 0 7px 14px 0 rgba(65,69,88,.1),0 3px 6px 0 rgba(0,0,0,.07);
  }
</style>