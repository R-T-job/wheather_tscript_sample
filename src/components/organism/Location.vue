<template>
  <div class="location">
    <h1 class="location-timezone">{{ locationTimezone }}</h1>
    <img class="wheather-icon" :src="wheatherIconSrc">
  </div>
</template>
<script lang="ts">
  import { defineComponent } from "@vue/composition-api";
  import {Component, Prop, Watch, Vue} from "vue-property-decorator";  

  @Component
  export default class Location extends Vue {
    @Prop() public locationTimezone!: string;
    @Prop() public wheatherIconSrc!: string;
  }
</script>
<style>
.location {
    height: 30vh;
    width: 50%;
    display: flex;
    justify-content: space-around;
    align-items: center;
}
</style>