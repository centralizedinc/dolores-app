<template>
  <a-layout>
    <a-back-top>
      <a-avatar>
        <a-icon type="up" :size="42"></a-icon>
      </a-avatar>
    </a-back-top>
    <a-layout-header class="header" :style="headerStyle">
      <a-row type="flex" justify="start" :gutter="8">
        <a-col :span="2">
          <a-avatar
            style="cursor:pointer"
            @click="$router.push('/')"
            src="https://i.postimg.cc/J47Nvpfn/Dolores-log.png"
            :size="50"
          ></a-avatar>
        </a-col>
        <a-col :span="4">
          <h3 style="color:#000000; margin-left: -6vh">Bayan ng Dolores</h3>
        </a-col>
        <a-col :span="2" :push="12">
          <a-button ghost block>NEWS</a-button>
        </a-col>
        <a-col :span="2" :push="12">
          <a-button ghost block>REPORT</a-button>
        </a-col>
        <a-col :span="2" :push="12">
          <a-button ghost block @click="signup_visible=true">SIGN-UP</a-button>
        </a-col>
      </a-row>
    </a-layout-header>
    <a-layout-content>
      <router-view></router-view>
    </a-layout-content>
    <a-layout-footer style="background: linear-gradient(to top, #469a25, #154102); color: #ffffff">
      <a-row>
        <a-col :span="24">
          <h1 style="color:#ffffff">Get in touch</h1>
          <!-- <a-divider></a-divider> -->
          <p>
            <a-icon type="phone" style="margin-right: 5px"></a-icon>Hotline: 123-3456
          </p>
          <p>
            <a-icon type="global" style="margin-right: 5px"></a-icon>Website:
            <a
              style="color:#ffffff"
              href="https://www.doloresquezon.gov.ph/"
            >https://www.doloresquezon.gov.ph/</a>
          </p>
          <p>
            <a-icon type="facebook" style="margin-right: 5px"></a-icon>Facebook:
            <a
              style="color:#ffffff"
              href="https://www.facebook.com/OrlanCalayagOfficial/"
            >Bayan ng Dolores</a>
          </p>
          <a-divider></a-divider>
        </a-col>

        <a-col :span="18">
          <p>© Copyright 2019 CCCI Inc. - All Rights Reserved</p>
        </a-col>
        <a-col :span="1">
          <a-avatar size="large" style="background-color:#4267B2">
            <a-icon type="facebook"></a-icon>
          </a-avatar>
        </a-col>
        <a-col :span="1">
          <a-avatar size="large" style="background-color:#EA4335">
            <a-icon type="google"></a-icon>
          </a-avatar>
        </a-col>
        <a-col :span="1">
          <a-avatar size="large" style="background-color:#4267B2">
            <a-icon type="twitter"></a-icon>
          </a-avatar>
        </a-col>
        <a-col :span="1">
          <a-avatar size="large" style="background:#00AFF0">
            <a-icon type="skype"></a-icon>
          </a-avatar>
        </a-col>
        <a-col :span="1">
          <a-avatar size="large" style="background-color:#FF2500">
            <a-icon type="youtube"></a-icon>
          </a-avatar>
        </a-col>
        <a-col :span="1">
          <a-avatar
            size="large"
            style="background:radial-gradient(circle at 30% 107%, #fdf497 0%, #fdf497 5%, #fd5949 45%,#d6249f 60%,#285AEB 90%);"
          >
            <a-icon type="instagram"></a-icon>
          </a-avatar>
        </a-col>
      </a-row>
    </a-layout-footer>
    <a-modal v-model="signup_visible" title="Register">
      <a-row type="flex" justify="center" :gutter="16">
        <a-col :span="24">
          <p>Register with facebook or google</p>
        </a-col>
        <a-col :span="12">
          <a-button
            block
            size="large"
            style="border: #4267B2;background-color:#4267B2; color:#FFFFFF"
            @click="registerFacebook"
          >
            <a-icon type="facebook"></a-icon>Facebook
          </a-button>
        </a-col>
        <a-col :span="12">
          <a-button
            block
            size="large"
            @click="registerGoogle"
            style="border: #DE4935;background-color:#DE4935; color:#FFFFFF"
          >
            <a-icon type="google"></a-icon>Google
          </a-button>
        </a-col>
        <a-col :span="24">
          <a-divider>Or</a-divider>
        </a-col>
        <a-col :span="24">
          <a-form>
            <a-form-item>
              <a-input placeholder="First Name"></a-input>
            </a-form-item>
            <a-form-item>
              <a-input placeholder="Last Name"></a-input>
            </a-form-item>
            <a-form-item>
              <a-input placeholder="Email"></a-input>
            </a-form-item>
            <a-form-item>
              <a-input placeholder="Password" type="password"></a-input>
            </a-form-item>
            <a-form-item>
              <a-input placeholder="Confirm Password" type="password"></a-input>
            </a-form-item>
          </a-form>
        </a-col>
      </a-row>
    </a-modal>
  </a-layout>
</template>

<script>
export default {
  data() {
    return {
      signup_visible: false,
      visible: false,
      topLocation: 0,
      reveal: false
    };
  },
  methods: {
    handleScroll(event) {
      // Any code to be executed when the window is scrolled
      console.log("event ::: ", JSON.stringify(window.top.scrollY));
      this.topLocation = window.top.scrollY;
    },
    registerFacebook() {
      window.open(
        `http://localhost:4000/auth/facebook`,
        "",
        "width=500,height=450"
      );
      this.signup_visible = false;
    },
    registerGoogle() {
      window.open(
        `http://localhost:4000/auth/google`,
        "",
        "width=500,height=450"
      );
      this.signup_visible = false;
    }
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
  destroyed() {
    window.removeEventListener("scroll", this.handleScroll);
  },

  computed: {
    headerStyle() {
      if (this.topLocation < 50) {
        return "background: transparent";
      } else {
        return "background: linear-gradient(to bottom, #469a25, #154102)";
      }
    }
  }
};
</script>

<style>
</style>