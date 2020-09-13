<template>
  <div class="temperature" @click="changeDegree()">
      <div class="degree-section">
        <h2 class="temprature-degree">{{ innerTempratureDegree }}</h2>
      <span>{{ degreeSpan }}</span>
    </div>
    <div class="temprature-description">{{ tempratureDescription }}</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed, reactive, ref, watch }  from "@vue/composition-api";
import {Component, Prop, Watch, Vue } from "vue-property-decorator";  

  type TempratureProp = {
    tempCentigrade: number
    tempratureDegree: number
    tempratureDescription: string
  };

  interface WeatherState {
    degreeSpan: string;
    innerTempratureDegree: number;
  }
  export default defineComponent({
    props: {
      tempCentigrade: {
        type: Number,
        default: 0
      },
      tempratureDegree: {
        type: Number,
        default: 0
      },
      tempratureDescription: {
        type: String,
        default: ""
      },
    },
    setup(props: TempratureProp, context) {

      let tempratureDescriptionValue = ref(props.tempratureDescription)
      let innerTempratureDegree =ref(props.tempratureDegree)
      let degreeSpan = "C"
      
      const changeDegree = () => {
        if(degreeSpan === "C"){
            degreeSpan = "F";
            let farenheit = (props.tempratureDegree) * (9 / 5) + 32
            innerTempratureDegree.value = Math.floor(farenheit);
        } else {
          degreeSpan = "C";
          innerTempratureDegree.value = props.tempratureDegree;
        }
      };

      watch(() => props.tempratureDegree, (newValue) => {
        innerTempratureDegree.value = newValue;
      });


      return {
        tempratureDescriptionValue,
        innerTempratureDegree,
        degreeSpan,
        changeDegree
      };
    }
  });
</script>

<style>
.temperature {
    height: 30vh;
    width: 50%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
}
.degree-section {
    display: flex;
    align-items: center;
}
.degree-section span {
    margin: 10px;
    font-size: 30px;
}
.degree-section h2 {
    font-size: 40px;
}
</style>