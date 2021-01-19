<template>
  <div class="index" :style="{backgroundColor: Back}" >
    <div id="top" class="container">
      <First :name="name" />
      <div class="nav-button">
        <el-button
          v-scroll-to="'#weather'"
          icon="el-icon-arrow-down"
          size="large"
        />
      </div>
    </div>

    <div id="weather" class="container">
      <Weather />
      <div class="nav-button">
        <el-button
          v-scroll-to="'#plan'"
          icon="el-icon-arrow-down"
          size="large"
        />
      </div>
    </div>

    <div id="plan" class="container">
      <Plan :mail="mail" :plans="plans" />
      <div class="nav-button">
        <el-button
          v-scroll-to="'#articles'"
          icon="el-icon-arrow-down"
          size="large"
        />
      </div>
    </div>

    <div id="articles" class="container">
      <Articles />
      <div class="nav-button">
        <el-button
          v-scroll-to="'#top'"
          icon="el-icon-arrow-down"
          size="large"
        />
      </div>
    </div>

    <div id="login">
      <el-button type="text" @click="login">Login</el-button>
    </div>

    <div id="color">
      <el-color-picker v-model="Back" @change="setBackground" ></el-color-picker>
    </div>

    <div id="cust-name">
      <el-button type="text" @click="customName" v-show="isLogin">Custom your name</el-button>
    </div>

  </div>
</template>

<script>
import Weather from "@/components/Weather.vue";
import First from "@/components/First.vue";
import Plan from "@/components/Plan.vue";
import Articles from "@/components/Articles.vue";

export default {
  components: {
    Weather,
    First,
    Plan,
    Articles,
  },
  data() {
    return {
      seq: [],
      name: "world",
      mail: "",
      plans: ["Plan 1", "Plan 2", "Plan 3"],
      Back: "#FFFFFF",
      isLogin: 0,
    };
  },
  methods: {
    async logData() {
      let recv = await this.$axios.$get("/userGet/" + this.mail);
      this.name = recv.name;
      this.seq = recv.sequence;
      this.plans = recv.plan;
      this.Back = '#' + recv.color;
      this.isLogin = 1;
    },

    async login() {
      await this.$prompt("Please input your e-mail", "Tip", {
        confirmButtonText: "OK",
        cancelButtonText: "Cancel",
        inputPattern: /[\w!#$%&'*+/=?^_`{|}~-]+(?:\.[\w!#$%&'*+/=?^_`{|}~-]+)*@(?:[\w](?:[\w-]*[\w])?\.)+[\w](?:[\w-]*[\w])?/,
        inputErrorMessage: "Invalid Email",
      })
        .then(({ value }) => {
          this.mail = value;
          this.$message({
            type: "success",
            message: "Welcome, " + value,
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "Login cancelled.",
          });
        });

      await this.logData();
    },

    async setBackground() {
      if (this.mail == "") {
        this.$notify.info({
          title: "Info",
          message: "Login to recognize your backgroubd color.",
        });
      } else {
        await this.$axios.$get("/color/" + this.mail + '/' + this.Back.split('#')[1]);
        this.$notify({
          title: "Success",
          message: "Change background color successfully.",
          type: "success",
          position: "top-left",
        });
      }
    },

    async customName() {
      await this.$prompt("Please input your name.", "Tip", {
        confirmButtonText: "OK",
        cancelButtonText: "Cancel",
      })
        .then(({ value }) => {
          this.name = value;
          this.$message({
            type: "success",
            message: "Welcome, " + value,
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "Login cancelled.",
          });
        });
      await this.$axios.$get("/name/" + this.mail + "/" + this.name);
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+TC&family=Ubuntu+Mono&display=swap");

.index {
  font-size: 40px;
  font-weight: 700;
}

@media only screen and (max-width: 576px) {
  .index {
  font-size: 30px;
  }
}

.index /deep/ .el-button {
  font-size: 20px;
  color: black;
}

.index /deep/ .el-button :hover {
  font-weight: 700;
}

</style>

<style scoped>
.container {
  margin: 0 auto;
  max-width: 100%;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  min-height: 100vh;
  align-items: center;
  font-family: "Noto Sans TC", sans-serif;
}

.nav-button {
  margin-top: auto;
  width: 100%;
  height: 10%;
}

.nav-button /deep/ .el-button {
  font-size: 80px;
  width: 100%;
  background: transparent;
  border: 0px;
  padding: 0;
}

#top,
#weather,
#plan,
#articles {
  flex-direction: row;
  justify-content: center;
  background-size: auto auto, auto auto;
  background-position: center center, center center;
  background-repeat: repeat-x, repeat-y;
}

#login {
  position: fixed;
  top: 10px;
  right: 30px;
}

#color {
  position: fixed;
  bottom: 80px;
  right: 30px;
}

#cust-name {
  position: fixed;
  bottom: 80px;
  right: 100px;

}
</style>
