<template>
  <div class="location">
    <h1 class="location-timezone">{{ locationTimezone }}</h1>
    <img class="wheather-icon" :src="wheatherIconSrc">
  </div>
</template>
<script lang="ts">
  import { defineComponent } from "@vue/composition-api";
  import {Component, Prop, Watch, Vue} from "vue-property-decorator";

  type LocationProp = {
    locationTimezone: string
    wheatherIconSrc: string
  };
  
  export default defineComponent({
    props: {
      locationTimezone: {
        type: String,
        default: ""
      },
      wheatherIconSrc: {
        type: String,
        default: ""
      },
    },
  });

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