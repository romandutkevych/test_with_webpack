<template>
  <div class="cb-item cb-item-3">
    <p class="cb-item__title">
      Цвет отпечатков
    </p>
    <p class="cb-item__text">
      наконец, подберите самые подходящие цвета красок, с помощью которых вы и оставите на
      картине свой след на память!<br>
      <strong>Обратите внимание: более 2-х цветов увеличат стоимость</strong>
    </p>

    <div class="cb-item-marks">
      <div v-for="(mark,index) in marks" v-bind:class="'cb-item-mark'">
        <input v-bind:id="mark.id" v-bind:type="'checkbox'" v-bind:value="index" v-on:change="chekmakr(index)"
               @click="marks[index].chacked = !marks[index].chacked">
        <label v-bind:for="mark.id" v-bind:title="mark.name"></label>
        <img v-bind:src="mark.imageLink" v-bind:alt="mark.name" width="136" height="136">
      </div>
    </div>
  </div>
</template>

<script>
    export default {
      props:["marks"],
      data(){
        return{
          chekedmark:{
            num:'',
          }
        }
      },
      methods:{
        chekmakr(index){
          this.chekedmark.num = index;
          this.$emit('change-mark',this.chekedmark.num);
        },
        meetchek(index){
          this.$emit('meet-mark',index);
        }
      }
    }
</script>

<style scoped>

</style>
