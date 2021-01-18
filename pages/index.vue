<template>
  <div>
    <div id="top" class="container">
      <First />
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
          v-scroll-to="'#water'"
          icon="el-icon-arrow-down"
          size="large"
        />
      </div>
    </div>

    <div id="water" class="container">
      <Water />
      <div class="nav-button">
        <el-button
          v-scroll-to="'#plan'"
          icon="el-icon-arrow-down"
          size="large"
        />
      </div>
    </div>

    <div id="plan" class="container">
      <Plan />
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
      <el-button type="text" @click="login">Login {{ this.seq }}</el-button>
    </div>
  </div>
</template>

<script>
import Weather from "@/components/Weather.vue";
import First from "@/components/First.vue";
import Water from "@/components/Water.vue";
import Plan from "@/components/Plan.vue";
import Articles from "@/components/Articles.vue";

export default {
  components: {
    Weather,
    First,
    Water,
    Plan,
    Articles,
  },
  data() {
    return {
      seq: [],
      name: "world",
      mail: "",
    };
  },
  methods: {
    async logData() {
      let recv = await this.$axios.$get("/userGet/" + this.mail);
      this.name = recv.name;
      this.seq = recv.sequence;
    },
    login() {
      this.$prompt("Please input your e-mail", "Tip", {
        confirmButtonText: "OK",
        cancelButtonText: "Cancel",
        inputPattern: /[\w!#$%&'*+/=?^_`{|}~-]+(?:\.[\w!#$%&'*+/=?^_`{|}~-]+)*@(?:[\w](?:[\w-]*[\w])?\.)+[\w](?:[\w-]*[\w])?/,
        inputErrorMessage: "Invalid Email",
      })
        .then(({ value }) => {
          this.mail = value;
          this.$message({
            type: "success",
            message: "Your email is:" + value,
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "Please login again.",
          });
        });

      this.logData();
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+TC&family=Ubuntu+Mono&display=swap");

.content-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  height: 90%;
  justify-content: center;
  align-items: center;
}

.title-container {
  margin: 2em 0em 6em 0em;
}

.content-container h1 {
  font-family: "Noto Sans TC", sans-serif;
  font-size: 40px;
  font-weight: 700;
}

.content-container h1.title-first-letter {
  position: absolute;
  right: 83.1%;
  color: #5d84af;
  background-color: #fae5c8;
  padding-left: 0.5em; /* left curve */
  padding-right: 0.2em; /* space between first and second letter */
  padding-top: 0.2em;
  padding-bottom: 0.2em;
  border-radius: 5em 0em 0em 5em;
}

.content-container h1.title-other-letter {
  position: absolute;
  left: 16.9%;
  color: #fae5c8;
  background-color: #5d84af;
  padding-right: 0.5em; /* left curve */
  padding-left: 0.2em; /* space between first and second letter */
  padding-top: 0.2em;
  padding-bottom: 0.2em;
  border-radius: 0em 4em 4em 0em;
}

.font-mono {
  font-family: "Ubuntu Mono", monospace;
}

@media only screen and (max-width: 976px) {
  .content-container h1 {
    font-size: 32px;
  }
}

@media only screen and (max-width: 576px) {
  .content-container h1 {
    font-size: 28px;
    font-weight: 600;
  }
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
#water,
#plan,
#articles {
  flex-direction: row;
  justify-content: center;
  /* background-image: url("/assets/background.png"), url("/assets/bar-background.png"); */
  background-size: 100% auto, 100% auto;
  background-position: center center, center center;
  background-repeat: no-repeat, repeat-y;
}

#login {
  position: fixed;
  top: 10px;
  right: 30px;
}
/* 
#articles{
  background-image: url("/assets/bar-background.png");
  background-size: 100% auto;
  background-repeat: repeat-y;
  display: inline;
} */

.fixed-container {
  position: fixed;
  width: 100px;
  height: 100px;
  z-index: 5;
  right: 40px;
  bottom: 40px;
}

.fixed-container /deep/ .el-button {
  padding: 20px;
  font-family: "Noto Sans TC", sans-serif;
  font-size: 30px;
  font-weight: 700;
  background: #f6d3d9;
  border: none;
}

.fixed-nav {
  position: fixed;
  top: 1%;
  left: 5%;
  width: 70px;
  display: flex;
  flex-direction: column;
  z-index: 5;
}

.fixed-nav /deep/ .el-button {
  padding-top: 10px;
  padding-left: 15px;
  border: none;
  font-family: "Noto Sans TC", sans-serif;
  font-size: 20px;
  font-weight: 600;
  letter-spacing: 3px;
  line-height: 25px;
  width: 80px;
  height: 80px;
  margin-top: 10px;
  background: #f3f3f3;
  color: #707070;
}

.fixed-nav /deep/ .el-button + .el-button {
  margin-left: 0;
}

.logo-button /deep/ .el-button {
  width: 130px;
  height: 130px;
  border: none;
  margin-bottom: 70%;
  margin-left: -20px;
  background-image: url("/assets/mc_logo.png");
  background-size: 100% auto;
}

@media only screen and (max-width: 576px) {
  .fixed-container {
    width: 60px;
    height: 60px;
    right: 5%;
    bottom: 5%;
  }

  .fixed-container /deep/ .el-button {
    padding-top: 15px;
    padding-left: 15px;
    width: 75px;
    height: 75px;
    font-size: 20px;
    font-weight: 600;
    letter-spacing: 3px;
    line-height: 23px;
  }

  .fixed-nav {
    left: 1%;
  }

  .fixed-nav /deep/ .el-button {
    padding-top: 8px;
    padding-left: 11px;
    width: 55px;
    height: 55px;
    font-size: 16px;
    font-weight: 500;
    letter-spacing: 1px;
    line-height: 18px;
  }

  .logo-button /deep/ .el-button {
    width: 60px;
    height: 60px;
    margin-left: 0;
  }
}

.award-button /deep/ .el-button {
  background: #ffc800;
  color: #f3752b;
  border: none;
}

.question-button /deep/ .el-button {
  background: #707070;
  color: #f3f3f3;
  border: none;
}
</style>
