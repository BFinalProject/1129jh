<template>
  <div>
    <NavHeader />
    <div class="container1" id="container1">
      <div class="form-container1 sign-up-container1">
        <form action="#">
          <h1>회원가입하기</h1>
          <div class="social-container1"></div>

          <div class="logins">
            성별&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
            <div class="form-check form-check-inline">
              <input
                class="form-check-input"
                type="radio"
                name="inlineRadioOptions"
                id="inlineRadio1"
                value="option1"
                style="
                  padding-right: 5px;
                  padding-left: 5px;
                  padding-top: 5px;
                  padding-bottom: 5px;
                "
              />
              <label class="form-check-label" for="inlineRadio1">남자</label>
            </div>
            <div class="form-check form-check-inline">
              <input
                class="form-check-input"
                type="radio"
                name="inlineRadioOptions"
                id="inlineRadio2"
                value="option2"
                style="
                  padding-right: 5px;
                  padding-left: 5px;
                  padding-top: 5px;
                  padding-bottom: 5px;
                "
              />
              <label class="form-check-label" for="inlineRadio2">여자</label>
            </div>
          </div>

          <input type="text" placeholder="이름" /><br />
          <input type="email" placeholder="아이디" /><br />

          <input
            type="password"
            id="password1"
            onchange="passwordreconfirm()"
            placeholder="비밀번호"
          /><br />
          <span id="pwConfirm" style="display: none"
            >입력한 글자가 6글자 이상이어야 합니다.</span
          >

          <input
            type="password"
            id="password2"
            onchange="passwordreconfirm()"
            placeholder="비밀번호확인"
          /><br />
          <!-- <span id="re" name="password2" onchange="alert(passwordreconfirm())"></span> -->
          <!-- onchange="alert(passwordreconfirm())" -->

          <span id="pwConfirm2" style="display: none"
            >비밀번호가 불일치 합니다.</span
          >
          <span id="pwConfirm3" style="display: none"
            >비밀번호가 일치 합니다.</span
          >

          <input type="email" placeholder="이메일" /><br />
          <input type="tel" placeholder="휴대폰번호" /> <br />
          <button type="button" class="button1">회원가입하기</button>
        </form>
      </div>
      <div class="form-container1 sign-in-container1">
        <form action="#">
          <h1>로그인</h1>
          <br />
          <input type="email" placeholder="아이디" />
          <br />
          <input type="password" placeholder="비밀번호" />
          <a href="#">아이디 혹은 비밀번호를 잊어버리셨나요?</a>

          <div class="login">
            <button type="button" class="button1" style="margin-bottom: 10px">
              로그인
            </button>

            <button type="button" class="kakao" @click="kakaoLogin()">
              <img
                src="../design/imageskakao/kakao_login/ko/kakao_login_medium_narrow.png"
              />
            </button>
          </div>
        </form>
      </div>
      <div class="overlay-container1">
        <div class="overlay">
          <div class="overlay-panel overlay-left">
            <h1>Welcome Back!</h1>
            <p>
              To keep connected with us please login with your personal info
            </p>
            <button type="button" class="button1" id="signIn">Sign In</button>
          </div>
          <div class="overlay-panel overlay-right">
            <h1>Hello, Friend!</h1>
            <p>아이디가 없으신가요?</p>
            <button type="button" class="button1" id="signUp">
              회원가입하기
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
@import "./login.css";
body {
  display: flex;
}
</style>
<script>
import NavHeader from "../views/NavHeader.vue";

export default {
  data: function() {
    return {
      // userList:[],
      // updatepassword:[]
    };
  },
  components: {
    NavHeader
  },

  created: function() {
    // console.log("created");
  },
  mounted: function() {
    let vm = this;
    // $('body').class
    // $('body').css({"display": "flex"});
  },
  methods: {
    kakaoLogin() {
      window.Kakao.Auth.login({
        scope: "account_email, gender, age_range",
        success: this.getKakaoAccount
      });
    },
    getKakaoAccount() {
      window.Kakao.API.request({
        url: "/v2/user/me",
        success: res => {
          const kakao_account = res.kakao_account;
          // const nickname = kakao_account.profile.nickname;
          const email = kakao_account.email;
          const gender = kakao_account.gender;
          const age_range = kakao_account.age_range;
          // console.log("nickname", nickname);
          console.log("email", email);
          console.log("gender", gender);
          console.log("age_range", age_range);
          // 로그인 처리 구현
          alert("로그인 성공!");
        },
        fail: error => {
          console.log(error);
        }
      });
      // fnUserInsertList: function(jsonObj) {
      //   this.$sendAxios("/user/insertUserList", jsonObj,
      //     function(resp){
      //         console.log(resp);
      //     });
      // },

      // fnUserUpdatePassword: function(jsonObj) {
      //   this.$sendAxios("/user/updatePassword", jsonObj,
      //     function(resp){
      //          console.log(resp);
      //         });
      //     },
    }
  }
};
</script>
