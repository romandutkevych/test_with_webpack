<template>
  <div class="cb-item cb-item-2">
    <p class="cb-item__title">
      Заголовок
    </p>
    <p class="cb-item__text">
      персонализируйте ваше "Дерево пожеланий"; вверху и внизу картины есть специальные поля,
      которые можно заполнить по вашему усмотрению: вписать имена виновников торжества, или
      особые пожелания, добавить дату, или логотип компании, если речь идет о корпоративном
      подарке.
    </p>
    <div class="cb-item__line">
      <input id="pic-title" @change="changeText" v-model="n_text.title" placeholder="Наша Свадьба" maxlength="22" type="text">
      <span>Заголовок картины</span>

    </div>
    <div class="cb-item__line">
      <input id="pic-name" @change="changeText" v-model="n_text.name" placeholder="Анастасия и Константин" maxlength="36" type="text">
      <span>Подпись</span>
    </div>
    <div class="cb-item__line">
      <input id="pic-date" @change="changeText"  v-model="n_text.date" placeholder="29 июля 2015" maxlength="26" type="text">
      <span>Дата события</span>
    </div>
    <div class="cb-item__line--btns">
      <span v-for="(font,index) in fonts"
            v-model="n_fonts.name"
            v-bind:class="['btn-font', {'btn-font--active': n_fonts.current === index}]"
            v-bind:id="font.toLowerCase()"
            @click="changeFont(index,font)">
        {{font}}</span>
    </div>
  </div>
</template>

<script>
    export default {
      props:["fonts"],
      data(){
        return{
          n_text:{
            title:'',
            name:'',
            date:''
          },
          n_fonts:{
            name: '',
            current: 0,
          }
        }

      },
      methods:{
        changeText:function(){
          if(this.n_text.title =='' && this.n_text.name =='' && this.n_text.age ==''){
            console.log('заповнити всі поля');
          }else{
            this.$emit('change-txt',this.n_text);
          }
        },
        changeFont:function(index,font){
          this.n_fonts.current = index;
          this.n_fonts.name = font;
          console.log(this.n_fonts.current);
          this.$emit('change-font',this.n_fonts.name)
        }

      }
    }
</script>

<style scoped>

</style>
