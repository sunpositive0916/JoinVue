<template>
  <JoinStepOne />
</template>

<script>
import JoinStepOne from "./components/JoinStepOne.vue";

export default {
  name: "App",
  components: {
    JoinStepOne,
  },
};
</script>

<style lang="scss">
.join-form {
  display: flex;
  align-items: center;
  position: relative;
  width: 100%;
  padding-bottom: 30px;
  font-size: 14px;

  &__title {
    width: 130px;
  }
  &__input {
    width: 200px;
    input {
      width: 100%;
      height: 30px;
      box-sizing: border-box;
    }
  }
}
</style>
