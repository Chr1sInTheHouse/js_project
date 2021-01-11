<template>
  <div>
    <p
      class="data"
      data-aos="fade-up"
      data-aos-anchor="#top"
      data-aos-delay="300"
      data-aos-anchor-placement="center-top"
    >
      Temperature: {{ temp }} °C
    </p>
    <p
      class="data"
      data-aos="fade-up"
      data-aos-anchor="#top"
      data-aos-delay="600"
      data-aos-anchor-placement="center-top"
    >
      降雨機率: {{ rain }} %
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      temp: 10,
      rain: 50,
    };
  },
};
</script>

<style>
</style>