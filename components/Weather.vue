<template>
  <div class="weather">
    <p
      class="text"
      data-aos="fade-up"
      data-aos-anchor="#top"
      data-aos-delay="300"
      data-aos-anchor-placement="center-top"
    >
      How's the weather today?
    </p>
    <p
      class="text"
      data-aos="fade-up"
      data-aos-anchor="#top"
      data-aos-delay="1000"
      data-aos-anchor-placement="center-top"
    >
      Temperature: {{ temp }} °C
    </p>
    <p
      class="text"
      data-aos="fade-up"
      data-aos-anchor="#top"
      data-aos-delay="1400"
      data-aos-anchor-placement="center-top"
    >
      {{ rain }}
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      temp: 10,
      rain: '',
    };
  },
  mounted: async function(){
      const temp = await this.$axios.$get('/temp');
      this.temp = temp;
      const rain = await this.$axios.$get('/rain');
      this.rain = rain;
      return temp;
  },
};
</script>

<style>
.weather {
  margin-left: 15%;
  margin-right: auto;
  margin-top: auto;
}
</style>