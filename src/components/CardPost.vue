<template>
  <div class="card">
    <h3 class="card__post-title text-primary">{{ title }}</h3>
    <p class="card__post-body">{{ body }}</p>
    <p class="card__author text-muted">{{ userName }}</p>
  </div>
</template>

<script>
export default {
  name: "CardPost",
  props: {
    title: String,
    body: String,
    userName: String,
  },
};
</script>

<style lang="less" scoped>
.card {
  width: 100%;
  padding: 10px 15px;
  margin-bottom: 30px;

  &__post-title {
    height: 68px;
    overflow: hidden;
  }

  &__post-body {
    height: 75px;
    overflow: hidden;
  }
}
</style>
