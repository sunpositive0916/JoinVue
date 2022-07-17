<template>
  <div>
    <div class="join-form join-form--card">
      <div class="join-form__title">
        <label for="inputcard">카드번호</label>
      </div>
      <div class="join-form__input">
        <input
          id="inputcard"
          type="text"
          v-model="signup.cardNum1"
          @blur="cardValid"
          maxlength="4"
          placeholder="앞 4자리"
        />
        <input
          type="text"
          v-model="signup.cardNum2"
          @blur="cardValid"
          maxlength="4"
          title="카드번호 5~8자리"
          placeholder="5~8자리"
        />
        <input
          type="text"
          v-model="signup.cardNum3"
          @blur="cardValid"
          maxlength="4"
          title="카드번호 9~12자리"
          placeholder="9~12자리"
        />
        <input
          type="text"
          v-model="signup.cardNum4"
          @blur="cardValid"
          maxlength="4"
          title="카드번호 13~16자리"
          placeholder="13~16자리"
        />
      </div>
      <span class="join-form__error" v-if="!cardValidFlag"
        >카드번호 형식이 맞지 않습니다.</span
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "JoinStepThree",
  data() {
    return {
      signup: {
        cardNum1: null,
        cardNum2: null,
        cardNum3: null,
        cardNum4: null,
      },
      cardValidFlag: true,
    };
  },
  methods: {
    cardValid() {
      if (
        /^[0-9]{4,}$/.test(this.signup.cardNum1) &&
        /^[0-9]{4,}$/.test(this.signup.cardNum2) &&
        /^[0-9]{4,}$/.test(this.signup.cardNum3) &&
        /^[0-9]{4,}$/.test(this.signup.cardNum4)
      ) {
        let cardNumber =
          this.signup.cardNum1 +
          this.signup.cardNum2 +
          this.signup.cardNum3 +
          this.signup.cardNum4;
        let totalNum = 0;

        cardNumber = cardNumber.split("");

        for (let i = cardNumber.length - 1; i >= 0; i--) {
          if (i % 2 === 0) {
            let doubleNum = cardNumber[i] * 2;
            if (doubleNum >= 10) {
              totalNum += parseInt(doubleNum) - 9;
            } else {
              totalNum += parseInt(doubleNum);
            }
          } else {
            totalNum += parseInt(cardNumber[i]);
          }
        }
        if (totalNum % 10 === 0) {
          this.cardValidFlag = true;
        } else {
          this.cardValidFlag = false;
        }
        console.log(totalNum);
      } else {
        this.cardValidFlag = false;
      }
    },
  },
};
</script>

<style lang="scss">
.join-form.join-form--card {
  display: block;
  .join-form__input {
    width: 100%;
    margin-top: 10px;
    input {
      width: 70px;
      margin-right: 5px;
    }
  }
}
</style>
