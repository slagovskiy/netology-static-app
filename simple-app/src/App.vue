<template>
  <div id="app">
    <CountDown />
    <p>app version 1.0.2</p>
  </div>
</template>

<script>
import CountDown from './components/CountDown.vue';

export default {
  name: 'App',
  components: {
    CountDown,
  },
};
</script>

<style lang="css">
body {
  background-color: #fafafa;
  margin: 0;
  padding: 20px;
}
</style>