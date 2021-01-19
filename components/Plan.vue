<template>
  <div class="plan">
    <p
      data-aos="fade-up"
      data-aos-anchor="#weather"
      data-aos-delay="300"
      data-aos-anchor-placement="center-top"
    >
      What's your plan today?
    </p>
    <el-input
      :placeholder="plans[0]"
      v-model="plans[0]"
      data-aos="fade-up"
      data-aos-anchor="#weather"
      data-aos-delay="500"
      data-aos-anchor-placement="center-top"
    ></el-input>
    <el-input
      :placeholder="plans[1]"
      v-model="plans[1]"
      data-aos="fade-up"
      data-aos-anchor="#weather"
      data-aos-delay="500"
      data-aos-anchor-placement="center-top"
    ></el-input>
    <el-input
      :placeholder="plans[2]"
      v-model="plans[2]"
      data-aos="fade-up"
      data-aos-anchor="#weather"
      data-aos-delay="500"
      data-aos-anchor-placement="center-top"
    ></el-input>
    <el-button
      type="text"
      @click="submit"
      data-aos="fade-up"
      data-aos-anchor="#weather"
      data-aos-delay="550"
      data-aos-anchor-placement="center-top"
    >
      Submit
    </el-button>
    <el-button
      type="text"
      @click="done"
      data-aos="fade-up"
      data-aos-anchor="#weather"
      data-aos-delay="550"
      data-aos-anchor-placement="center-top"
    >
      Done
    </el-button>
  </div>
</template>

<script>
export default {
  props: ["mail", "plans"],
  methods: {
    async submit() {
      if (this.$props.mail == "") {
        this.$notify.info({
          title: "Info",
          message: "Please login first.",
        });
      } else {
        await this.$axios.$get(
          "/plan/" + this.$props.mail + "/" + this.$props.plans.toString()
        );
        this.$notify({
          title: "Success",
          message: "Submit successfully.",
          type: "success",
          position: "top-left",
        });
      }
    },
    async done() {
      if (this.$props.mail == "") {
        this.$notify.info({
          title: "Info",
          message: "Please login first.",
        });
      } else {
        this.$notify({
          title: "Congratulation! ",
          message: "You have done your plans. Keep going!",
          type: "success",
          position: "top-left",
        });
      }
    },
  },
};
</script>

<style>
.plan {
  margin-left: 10%;
  margin-right: auto;
  margin-top: 20%;
}
</style>