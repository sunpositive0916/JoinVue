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
    <div class="join-form join-form--address">
      <div class="join-form__title"><label for="inputaddress">주소</label></div>
      <div class="join-form__input">
        <button
          type="button"
          id="inputaddress"
          class="button__zip"
          @click="execDaumPostcode()"
        >
          우편번호 찾기
        </button>
        <input
          type="text"
          v-model="signup.addressBasic"
          readonly
          title="도로명 주소"
        />
        <input
          type="text"
          v-model="signup.addressDetail"
          title="상세 주소"
          placeholder="상세주소 입력"
        />
      </div>
    </div>
    <div class="bottom-button">
      <button type="button" :disabled="nextPageDisabled" @click="goToStepThree">
        다음
      </button>
      <button type="button" :disabled="nextPageDisabled" @click="goToStepOne">
        이전
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "JoinStepTwo",
  props: ["nameValue", "phoneValue", "addressBasicValue", "addressDetailValue"],
  data() {
    return {
      signup: {
        name: this.nameValue,
        phone: this.phoneValue,
        addressBasic: this.addressBasicValue,
        addressDetail: this.addressDetailValue,
      },
      nameValidFlag: true,
      phoneValidFlag: true,
    };
  },
  computed: {
    nextPageDisabled() {
      if (
        this.isEmpty(this.signup.name) ||
        this.isEmpty(this.signup.phone) ||
        this.isEmpty(this.signup.addressBasic) ||
        this.isEmpty(this.signup.addressDetail)
      ) {
        return true;
      }
      if (!this.nameValidFlag || !this.phoneValidFlag) {
        return true;
      }
      return false;
    },
  },
  methods: {
    isEmpty(data) {
      if (data === "" || data === null || data === undefined) {
        return true;
      } else {
        return false;
      }
    },
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
    execDaumPostcode() {
      new window.daum.Postcode({
        oncomplete: (data) => {
          // 팝업에서 검색결과 항목을 클릭했을때 실행할 코드를 작성하는 부분.

          // 도로명 주소의 노출 규칙에 따라 주소를 표시한다.
          // 내려오는 변수가 값이 없는 경우엔 공백('')값을 가지므로, 이를 참고하여 분기 한다.
          let roadAddr = data.roadAddress; // 도로명 주소 변수
          let extraRoadAddr = ""; // 도로명 조합형 주소 변수

          // 법정동명이 있을 경우 추가한다. (법정리는 제외)
          // 법정동의 경우 마지막 문자가 "동/로/가"로 끝난다.
          if (data.bname !== "" && /[동|로|가]$/g.test(data.bname)) {
            extraRoadAddr += data.bname;
          }
          // 건물명이 있고, 공동주택일 경우 추가한다.
          if (data.buildingName !== "" && data.apartment === "Y") {
            extraRoadAddr +=
              extraRoadAddr !== ""
                ? ", " + data.buildingName
                : data.buildingName;
          }
          // 표시할 참고항목이 있을 경우, 괄호까지 추가한 최종 문자열을 만든다.
          if (extraRoadAddr !== "") {
            extraRoadAddr = " (" + extraRoadAddr + ")";
          }
          // 참고항목 문자열이 있을 경우 해당 필드에 넣는다.
          if (roadAddr !== "") {
            roadAddr += extraRoadAddr;
          }

          this.signup.addressBasic = roadAddr;
        },
      }).open();
    },
    goToStepOne() {
      this.$emit(
        "goToStepOne",
        this.signup.name,
        this.signup.phone,
        this.signup.addressBasic,
        this.signup.addressDetail
      );
    },
    goToStepThree() {
      this.$emit(
        "goToStepThree",
        this.signup.name,
        this.signup.phone,
        this.signup.addressBasic,
        this.signup.addressDetail
      );
    },
  },
};
</script>

<style lang="scss">
.join-form.join-form--address {
  .join-form__input {
    width: 300px;
    input {
      margin-top: 5px;
    }
  }
}
.button__zip {
  width: 100px;
  height: 30px;
  border: 1px solid #919191;
  background: #fff;
  border-radius: 4px;
  cursor: pointer;
  box-sizing: border-box;
  &:hover {
    text-decoration: underline;
  }
}
</style>
