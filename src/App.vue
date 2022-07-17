<template>
  <JoinStepOne
    :emailValue="email"
    :cardNum1Value="cardNum1"
    :cardNum2Value="cardNum2"
    :cardNum3Value="cardNum3"
    :cardNum4Value="cardNum4"
    v-on:goToStepTwo="goToStepTwo"
    v-if="joinOneCheck"
  />
  <JoinStepTwo
    :nameValue="name"
    :phoneValue="phone"
    :addressBasicValue="addressBasic"
    :addressDetailValue="addressDetail"
    v-on:goToStepOne="goToStepOne"
    v-on:goToStepThree="goToStepThree"
    v-if="joinTwoCheck"
  />
  <JoinStepThree
    :emailValue="email"
    :cardNum1Value="cardNum1"
    :cardNum2Value="cardNum2"
    :cardNum3Value="cardNum3"
    :cardNum4Value="cardNum4"
    v-on:goToStepTwo="goToStepTwo"
    v-on:goToStepComplete="goToStepComplete"
    v-if="joinThreeCheck"
  />
  <JoinStepComplete
    :nameValue="name"
    :emailValue="email"
    :addressBasicValue="addressBasic"
    :addressDetailValue="addressDetail"
    :phoneValue="phone"
    v-if="joinCompleteCheck"
  />
</template>

<script>
import JoinStepOne from "./components/JoinStepOne.vue";
import JoinStepTwo from "./components/JoinStepTwo.vue";
import JoinStepThree from "./components/JoinStepThree.vue";
import JoinStepComplete from "./components/JoinStepComplete.vue";

export default {
  name: "App",
  components: {
    JoinStepOne,
    JoinStepTwo,
    JoinStepThree,
    JoinStepComplete,
  },
  data: function () {
    return {
      email: "",
      name: "",
      phone: "",
      addressBasic: "",
      addressDetail: "",
      cardNum1: "",
      cardNum2: "",
      cardNum3: "",
      cardNum4: "",
      joinOneCheck: true,
      joinTwoCheck: false,
      joinThreeCheck: false,
      joinCompleteCheck: false,
    };
  },
  methods: {
    goToStepOne(name, phone, addressBasic, addressDetail) {
      this.joinOneCheck = true;
      this.joinTwoCheck = false;
      this.name = name;
      this.phone = phone;
      this.addressBasic = addressBasic;
      this.addressDetail = addressDetail;
    },
    goToStepTwo(email, cardNum1, cardNum2, cardNum3, cardNum4) {
      this.joinOneCheck = false;
      this.joinTwoCheck = true;
      this.joinThreeCheck = false;
      this.email = email;
      this.cardNum1 = cardNum1;
      this.cardNum2 = cardNum2;
      this.cardNum3 = cardNum3;
      this.cardNum4 = cardNum4;
    },
    goToStepThree(name, phone, addressBasic, addressDetail) {
      this.joinTwoCheck = false;
      this.joinThreeCheck = true;
      this.name = name;
      this.phone = phone;
      this.addressBasic = addressBasic;
      this.addressDetail = addressDetail;
    },
    goToStepComplete() {
      this.joinThreeCheck = false;
      this.joinCompleteCheck = true;
    },
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
      vertical-align: top;
    }
  }

  &__error {
    position: absolute;
    left: 0;
    bottom: 12px;
    font-size: 12px;
    color: red;
  }
}

.bottom-button {
  display: flex;
  justify-content: space-between;
  width: 300px;
  button {
    width: 50px;
    height: 30px;
    background: #000;
    color: #fff;
    border: 0;
    cursor: pointer;
    box-sizing: border-box;
    &:hover {
      background: #be9162;
    }
  }
}
</style>
