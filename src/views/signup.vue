<template>
  <div class="home">
    회원 가입
    <br />
    <br />

    <!-- <div class="rule pa-0 ma-0">
      <div class="include justify-center pa-0 ma-0">
        <v-text-field
          hide-details
          class="setinput pa-0 ma-0 hide-details"
          v-model="form.name"
          type="text"
          placeholder="이름"
        >
        </v-text-field>
      </div>
    </div> -->
  
    <div class="rule pa-0 ma-0">
      <div class="include justify-center pa-0 ma-0 hide-details">
        <v-text-field
          hide-details
          class="setinput pa-0 ma-0"
          v-model="form.email"
          type="text"
          placeholder="이메일"
        >
        </v-text-field>
      </div>
    </div>
 
    <div class="rule pa-0 ma-0">
      <div class="include justify-center pa-0 ma-0">
        <v-text-field
          hide-details
          class="setinput pa-0 ma-0 hide-details"
          v-model="form.password"
          type="text"
          placeholder="비밀번호"
        >
        </v-text-field>
      </div>
    </div>
    <!-- <div class="rule pa-0 ma-0">
      <div class="include justify-center pa-0 ma-0">
        <v-text-field
          hide-details
          class="setinput pa-0 ma-0 hide-details"
          v-model="form.passwordConfirm"
          type="text"
          placeholder="비밀번호 확인"
        >
        </v-text-field>
      </div>
    </div>
    <div class="rule pa-0 ma-0">
      <div class="include justify-center pa-0 ma-0">
        <v-text-field
          hide-details
          class="setinput pa-0 ma-0 hide-details"
          v-model="form.firaddress"
          type="text"
          placeholder="주소(시,도 단위)"
        >
        </v-text-field>
      </div>
    </div>
    <div class="rule pa-0 ma-0">
      <div class="include justify-center pa-0 ma-0">
        <v-text-field
          hide-details
          class="setinput pa-0 ma-0 hide-details"
          v-model="form.secaddress"
          type="text"
          placeholder="주소(군,구 단위)"
        >
        </v-text-field>
      </div>
    </div>
    <div class="rule pa-0 ma-0">
      <div class="include justify-center pa-0 ma-0">
        <v-text-field
          hide-details
          class="setinput pa-0 ma-0 hide-details"
          v-model="form.thraddress"
          type="text"
          placeholder="주소(읍,면,동 단위)"
        >
        </v-text-field>
      </div>
    </div> -->
    <br />
    <br />
    <v-btn @click="onSubmit"> 가입하기 </v-btn>
  </div>
</template>

<script>
import { mapState, mapActions, mapMutations } from "vuex";
import axios from "axios";
import { ValidationProvider } from "vee-validate";

export default {
  components: {
    ValidationProvider,
  },

  data() {
    return {
      form: {
        email: "",
        password: "",
        passwordConfirm: "",
        name: "",
        firaddress: "",
        secaddress: "",
        thraddress: ""
      },

      userlist: [],
    };
  },

  methods: {
    async onSubmit() {
      try {
        await axios.post("http://localhost:5300/users/create", {
          email: this.form.email,
          password: this.form.password,
     
        });
      } catch (err) {
        console.log(err);
      }

      // this.form.email = "";
      // this.form.password = "";


      this.$router.push({ name: "login" });
    },

    whileread() {
      axios
        .get("/signup/account")
        .then((r) => {
          this.userlist = r.data.posts;
          console.log(r.data.posts);
        })
        .catch((e) => {
          console.error(e.message);
        });
    },

    checklogin() {
      this.$router.push({ name: "linkedinfo" });
    },
  },
};
</script>
<style>
.setinput {
  width: 200px;
}

.include {
  display: flex;
  justify-content: center;
  width: 200px;
}

.rule {
  display: flex;

  justify-content: center;
}
</style>