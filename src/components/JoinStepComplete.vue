<template>
  <div>
    <p>'{{ this.nameValue }}'님</p>
    <p>회원가입 되었습니다.</p>
    <p>이메일 : {{ this.emailValue }}</p>
    <p>주소 : {{ this.addressBasicValue + " " + this.addressDetailValue }}</p>
    <p>연락처 : {{ this.phoneValue }}</p>
  </div>
</template>

<script>
export default {
  name: "JoinStepComplete",
  props: [
    "nameValue",
    "emailValue",
    "addressBasicValue",
    "addressDetailValue",
    "phoneValue",
  ],
  data() {},
  computed: {},
  methods: {},
};
</script>
