<template>
  <div>
    <div class="join-form join-form--email">
      <div class="join-form__title"><label for="inputemail">이메일</label></div>
      <div class="join-form__input">
        <input
          id="inputemail"
          v-model="signup.email"
          type="text"
          maxlength="20"
          @blur="emailValid"
        />
      </div>
      <span class="join-form__error" v-if="!emailValidFlag"
        >이메일 주소의 형식이 맞지 않습니다.</span
      >
    </div>
    <div class="join-form join-form--password">
      <div class="join-form__title">
        <label for="inputpass">비밀번호</label>
      </div>
      <div class="join-form__input">
        <input
          id="inputpass"
          v-model="signup.password"
          type="password"
          maxlength="16"
          @blur="passwordValid"
        />
      </div>
      <span class="join-form__error" v-if="!passwordValidFlag"
        >영문 대문자, 소문자, 특수문자를 포함한 8자리 이상, 16자리 이하의
        비밀번호를 설정해주세요.</span
      >
    </div>
    <div class="join-form join-form--password">
      <div class="join-form__title">
        <label for="inputpasscheck">비밀번호 확인</label>
      </div>
      <div class="join-form__input">
        <input
          id="inputpasscheck"
          v-model="passwordCheck"
          type="password"
          maxlength="16"
          @blur="passwordCheckValid"
        />
      </div>
      <span class="join-form__error" v-if="!passwordCheckFlag"
        >비밀번호가 동일하지 않습니다.</span
      >
    </div>
    <div class="bottom-button">
      <button type="button" @click="goToStepTwo">다음</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "JoinStepOne",
  props: [
    "emailValue",
    "cardNum1Value",
    "cardNum2Value",
    "cardNum3Value",
    "cardNum4Value",
  ],
  data() {
    return {
      signup: {
        email: this.emailValue,
        password: null,
      },
      emailValidFlag: true,
      passwordCheck: null,
      passwordValidFlag: true,
      passwordCheckFlag: true,
    };
  },
  methods: {
    emailValid() {
      if (
        // eslint-disable-next-line
        /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/.test(
          this.signup.email
        )
      ) {
        this.emailValidFlag = true;
      } else {
        this.emailValidFlag = false;
      }
    },
    passwordValid() {
      if (
        // eslint-disable-next-line
        /^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\"]).{8,16}$/.test(
          this.signup.password
        )
      ) {
        this.passwordValidFlag = true;
      } else {
        this.passwordValidFlag = false;
      }
    },
    passwordCheckValid() {
      if (this.signup.password === this.passwordCheck) {
        this.passwordCheckFlag = true;
      } else {
        this.passwordCheckFlag = false;
      }
    },
    goToStepTwo() {
      this.$emit(
        "goToStepTwo",
        this.signup.email,
        this.cardNum1Value,
        this.cardNum2Value,
        this.cardNum3Value,
        this.cardNum4Value
      );
    },
  },
};
</script>
