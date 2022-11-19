<template>
  <div id="app">
    <h1>Style Transfer with Arbitrary Text</h1>
    <UploadImageContainer />
  </div>
</template>

<script>
import UploadImageContainer from "@/components/UploadImageContainer";
export default {
  name: 'App',
  components: {
    UploadImageContainer
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
