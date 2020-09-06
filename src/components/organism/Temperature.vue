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
import {Component, Prop, Watch, Vue} from "vue-property-decorator";  

@Component
export default class Temperature extends Vue {
  private degreeSpan: string = "C";
  private innerTempratureDegree: number = 0;

  @Prop()　public tempCentigrade!: number;
  @Prop()　public tempratureDegree!: number;
  @Prop()　public tempratureDescription!: string;

  changeDegree(){
    if(this.degreeSpan === "C"){
      this.degreeSpan = "F";
      let farenheit = (this.tempratureDegree) * (9 / 5) + 32
      this.innerTempratureDegree = Math.floor(farenheit);
    } else {
      this.degreeSpan = "C";
      this.innerTempratureDegree = this.tempCentigrade;
    }
  }
  @Watch('tempratureDegree', {immediate: true})
  private changeTempratureDegree(value: number){
    this.innerTempratureDegree = value;
  }
}
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