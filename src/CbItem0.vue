<template>
  <div class="cb-item cb-item-0">
    <p class="cb-item__title">
      Выберите изображение
    </p>
    <p class="cb-item__text">
      для начала выберите основу, саму картину, на которую вы и гости вашего праздника будете
      наносить отпечатки пальцев с пожеланиями
    </p>
    <div class="cb-item-pics">
      <div v-for="(picture,index) in pictures"
           v-bind:class="'cb-item-pic cb-item-pic'+index"
           v-on:click="takePict(index)">
        <!--<p>{{picture.name}}</p>-->
        <img v-bind:src="picture.imageLink" v-bind:title="picture.name" v-bind:alt="picture.name"  width="176"
             height="220">
      </div>
    </div>
  </div>
</template>

<script>
    export default {
      props:["pictures"],
      methods:{
        takePict(index){
          this.$emit('take-pict', index);
        }
      }
    }
</script>

<style scoped>

</style>
