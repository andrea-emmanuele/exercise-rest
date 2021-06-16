<template>
  <div class="card">
    <div class="header">
      <div class="inner-header">
        <h4>Running Jobs</h4>
        <h4>Current Status</h4>
      </div>
    </div>
    <div class="content">
      <div class="item">
        <div class="item-name">{{ job.name }}</div>
        <div :class="isSuccess" class="item-status">{{ job.status }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["heading", "job"],
  computed: {
    isSuccess() {
      return {
        success: this.job.status === "Success"
      }
    }
  }
};
</script>

<style scoped lang="scss">
  .card {
    max-width: 35%;
    height: 100px;
    background: $card_bg;
    border-radius: 0.5rem;
    overflow: hidden;
    margin: 0 auto;
    box-shadow: 0 7px 14px 0 rgba(65,69,88,.1),0 3px 6px 0 rgba(0,0,0,.07);

    > .header {
      background: $card_header_bg;
      > .inner-header {
        padding: $card_inner_py $card_inner_px;
        display: flex;
        justify-content: space-between;
      }
    }
    > .content {
      padding: $card_inner_py $card_inner_px;
      > .item {
        display: flex;
        justify-content: space-between;

        > .item-name,
          .item-status {
          text-align: center;
          width: 100px;
        }

        > .item-status {
          &.success {
            font-weight: bold;
            color: $success-color;
            animation: growUp 200ms ease-in-out;

            @keyframes growUp {
              from {
                transform: scale(1);
              }
              to {
                transform: scale(1.2);
              }
            }
          }
        }
      }
    }
  }
</style>