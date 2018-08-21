<template>
  <div class="cb-item cb-item-1">
    <p class="cb-item__title">
      Рама
    </p>
    <p class="cb-item__text">
      подберите раму, которая подойдет случаю и впишется в интерьер, ведь вы же не просто
      оставляете "пальчики", а создаете предмет декора для дома и офиса:
    </p>
    <div class="cb-item-borders">
      <div v-for="(border,index) in borders"
           v-bind:class="'cb-item-border cb-item-border'+index"
           v-on:click="takeBorder(index)">
        <!--<p>{{picture.name}}</p>-->
        <img v-bind:src="border.imageLink" v-bind:title="border.name" v-bind:alt="border.name"  width="176"
             height="220">
      </div>
    </div>
  </div>
</template>

<script>
    export default {
      props:["borders"],
      methods:{
        takeBorder:function (index) {
          this.$emit('take-border',index)
        }
      }
    }
</script>

<style scoped>

</style>
