<template>
  <div class="root">
    <div class="weather-root">
      <input type="text" class="input-box">
    </div>
    
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Weather extends Vue {
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.root {
  min-height: 100vh;
  background-image: url('https://images.unsplash.com/photo-1530908295418-a12e326966ba?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1534&q=80');
}
.weather-root {
  max-width: 500px;
  margin: auto;
  display: flex;
  justify-content: center;
}
.input-box {
  font-size: 25px;
}
</style>
