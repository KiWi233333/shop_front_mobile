<template>
  <div class="animate__animated animate__fadeInLeft v-card CardGroup">
    <div class="v-click left-card" @click="toView('order')">
      <div class="left">
        <span>我的订单</span>
        <span>查看最近订单</span>
      </div>
      <img src="@/assets/image/bg/order_bg.png" class="bg" />
    </div>
    <span style="border: 1px solid var(--bg-color3); height: 1.8rem"></span>
    <div class="v-click right-card" @click="toView('collect')">
      <div class="left">
        <span>收藏商品</span>
        <span>查看最近收藏</span>
      </div>
      <img src="@/assets/image/bg/collect_bg.png" class="bg" />
    </div>
  </div>
</template>
<script>
export default {
  name: "CardGroup",
  data() {
    return {};
  },
  methods: {
    // 二级页面跳转
    toView(target) {
      this.$router.push({
        name: this.$store.getters.token !== "" ? target : "login",
        params: {
          animate: "forward",
          toBack: true,
        },
      });
    },
  },
};
</script>
<style scoped>
.CardGroup {
  animation-delay: calc(var(--router-delay) / 1.5);
  display: flex;
  align-items: center;
  margin: 0.4rem 0;
  width: 100%;
}
.left-card,
.right-card {
  display: flex;
  width: 50%;
  justify-content: space-around;
  align-items: center;
  padding: 0.4rem 0.2rem;
  cursor: pointer;
}
.left {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.left span:nth-child(2) {
  font-size: 0.3rem;
  opacity: 0.6;
}
.CardGroup img {
  display: block;
  height: 1.1rem;
  padding: 0.1rem;
  object-fit: cover;
}
</style>