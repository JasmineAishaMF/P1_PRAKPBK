<template>
  <div id="app">
    <BiodataForm />
  </div>
</template>

<script>
import BiodataForm from './components/BiodataForm.vue'

export default {
  name: 'App',
  components: {
    BiodataForm
  }
}
</script>

<style>
/* P1_PraktikumPBK/src/App.vue */
body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  padding: 20px;
  margin: 0;
}
</style>