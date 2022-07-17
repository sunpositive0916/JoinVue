<template>
  <div>
    <div class="join-form join-form--email">
      <div class="join-form__title"><label for="inputemail">이메일</label></div>
      <div class="join-form__input">
        <input id="inputemail" type="text" />
      </div>
    </div>
    <div class="join-form join-form--password">
      <div class="join-form__title">
        <label for="inputpass">비밀번호</label>
      </div>
      <div class="join-form__input">
        <input id="inputpass" type="password" />
      </div>
    </div>
    <div class="join-form join-form--password">
      <div class="join-form__title">
        <label for="inputpasscheck">비밀번호 확인</label>
      </div>
      <div class="join-form__input">
        <input id="inputpasscheck" type="password" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "JoinStepOne",
  data() {},
  computed: {},
  methods: {},
};
</script>
