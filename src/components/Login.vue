<template>
  <Page loaded="pageLoaded" actionBarHidden="true">
    <ActionBar title="Login" />
    <FlexboxLayout class="page" backgroundColor="#ffff">
      <StackLayout width="400" class="form">
        <Image  class="logo" src="~/assets/images/profile.png" />

        <StackLayout class="input-field"  marginTop="80" marginBottom="25">
          <TextField
            class="input"
            hint="Email@email.com"
            keyboardType="email"
            autocorrect="false"
            autocapitalizationType="none"
            v-model="user1"
            returnKeyType="next"
            @returnPress="focusPassword"
            fontSize="18"
          />
          <StackLayout class="hr-light" />
        </StackLayout>

        <StackLayout class="input-field"  marginBottom="25">
          <TextField
            ref="password"
            class="input"
            hint="Password"
            secure="true"
            v-model="pass"
            :returnKeyType="isLoggingIn ? 'done' : 'next'"
            @returnPress="focusConfirmPassword"
            fontSize="18"
          />
          <StackLayout class="hr-light" />
        </StackLayout>

        <StackLayout v-show="!isLoggingIn" class="input-field">
          <TextField
            ref="confirmPassword"
            class="input"
            hint="Confirm password"
            secure="true"
            v-model="confirmPass"
            returnKeyType="done"
            fontSize="18"
          />
          <StackLayout class="hr-light" />
        </StackLayout>

        <Button
          :text="isLoggingIn ? 'Đăng nhập' : 'Đăng kí'"
          @tap="submit()"
          class="btn btn-primary m-t-20"
          height="80"
        />
        <Label
          v-show="isLoggingIn"
          text="Bạn quên mật khẩu ?"
          class="login-label"
          @tap="forgotPassword"
          marginTop="10"
          color="blue"
        />
      </StackLayout>

      <Label
        class="login-label sign-up-label"
        @tap="toggleForm"
        marginBottom="10"
      >
        <FormattedString>
          <Span
            :text="
              isLoggingIn ? 'Bạn chưa có tài khoản? ' : 'Trở lại Đăng nhập'
            "
          />
          <Span :text="isLoggingIn ? 'Sign up' : ''" class="bold" color="blue" />
        </FormattedString>
      </Label>
    </FlexboxLayout>
  </Page>
</template>

<script >
import App from "./app";
export default {
  data() {
    return {
      isLoggingIn: true,
      user1: "",
      pass: "",
      confirmPass: "",
      // gia su co 1 dối tuọng
      users: [
        {
          user: "ly",
          password: "itc",
          conformPassWord: "itc",
        },
      ],
    };
  },
  // tính số dòng
  methods: {
    submit() {
      if (
        this.user1.localeCompare(this.users.user) &&
        this.pass.localeCompare(this.users.password)
      ) {
        console.log("hhhhh-------------------" + this.user1);
        this.$navigateTo(App, {
          props: {
            user: this.user1,
          },
        });
      }
    },
    toggleForm() {
      this.isLoggingIn = !this.isLoggingIn;
    },
    focusPassword() {
      this.$refs.password.nativeView.focus();
    },
    focusConfirmPassword() {
      if (!this.isLoggingIn) {
        this.$refs.confirmPassword.nativeView.focus();
      }
    },
    handleLogin() {
      let d = 0;
      let users = appSettings.getString("users", "[]")
        ? JSON.parse(appSettings.getString("users", "[]"))
        : [];
      console.log(JSON.parse(appSettings.getString("users", "[]")));
      users.forEach((u) => {
        if (this.user === u.user && this.pass === u.pass) {
          appSettings.setBoolean("isLogin", true);
          appSettings.setString("user", JSON.stringify(u));
          alert("Đăng nhập thành công");
          this.$navigateTo(App, {
            animated: true,
            transition: {
              name: "slideRight",
              duration: 250,
              curve: "easeIn",
            },
            props: {
              user: u,
            },
          });
        } else {
          d++;
        }
      });
      if (d == users.length) {
        alert("Sai tên đăng nhập hoặc mật khẩu");
      }
    },
  },
};
</script>

<style scoped>
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}

.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
Image {
  text-align: center;
  width: 100;
  height: 100;
}
.page {
  align-items: center;
  flex-direction: column;
}
.form {
  margin-left: 30;
  margin-right: 30;
  flex-grow: 2;
  vertical-align: middle;
}


.logo{
  margin-top: -200;
}
</style>
