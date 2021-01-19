<template>
  <div class="hello">
    Hello, {{ name }}!
  </div>
</template>

<script>
export default {
  props: ["name"],
};
</script>

<style>
.hello {
  margin-left: auto;
  margin-right: 20%;
  margin-top: auto;
}
</style>