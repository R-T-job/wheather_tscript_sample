<template>
  <div id="app">
    <WeatherTemplate />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import WeatherTemplate from '@/components/templates/WeatherTemplate.vue';


@Component({
  components: {
    WeatherTemplate,
  },
})
export default class App extends Vue {}
</script>

<style>
</style>