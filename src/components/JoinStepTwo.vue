<template>
  <div>
    <div class="join-form join-form--name">
      <div class="join-form__title"><label for="inputName">이름</label></div>
      <div class="join-form__input">
        <input
          id="inputName"
          v-model="signup.name"
          type="text"
          maxlength="20"
          @blur="nameValid"
        />
      </div>
      <span class="join-form__error" v-if="!nameValidFlag"
        >이름 형식이 맞지 않습니다.</span
      >
    </div>
    <div class="join-form join-form--phone">
      <div class="join-form__title"><label for="inputPhone">연락처</label></div>
      <div class="join-form__input">
        <input
          id="inputPhone"
          v-model="signup.phone"
          type="text"
          maxlength="16"
          @blur="phonedValid"
        />
      </div>
      <span class="join-form__error" v-if="!phoneValidFlag"
        >휴대전화 번호 형식이 맞지 않습니다.</span
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "JoinStepTwo",
  data() {
    return {
      signup: {
        name: null,
        phone: null,
        addressBasic: null,
        addressDetail: null,
      },
      nameValidFlag: true,
      phoneValidFlag: true,
    };
  },
  methods: {
    nameValid() {
      if (/^[가-힣]{2,}|[a-zA-z]{3,}$/.test(this.signup.name)) {
        this.nameValidFlag = true;
      } else {
        this.nameValidFlag = false;
      }
    },
    phonedValid() {
      if (
        /^01([0|1|6|7|8|9])(-| )?([0-9]{3,4})(-| )?([0-9]{4})$/.test(
          this.signup.phone
        )
      ) {
        this.phoneValidFlag = true;
      } else {
        this.phoneValidFlag = false;
      }
    },
  },
};
</script>
