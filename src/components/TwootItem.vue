<template>
  <div class="twoot-item">
    <h2>{{ twootDate }}</h2>

    <div class="twoot-item__content">
      {{ twoot.content }}
    </div>
  </div>
</template>

<script>
export default {
  name: "TwootItem",
  props: {
    twootDate: {
      type: String,
      required: true
    },
    twoot: {
      type: Object,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.twoot-item {
  padding: 20px;
  margin: 0 auto 10px;
  background-color: #fff;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
  cursor: pointer;
  transition: all 0.3s ease;

  &:hover {
    transform: scale(1.05);
  }
}
</style>
