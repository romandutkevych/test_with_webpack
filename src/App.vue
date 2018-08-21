<template>
  <div id="app">
    <div class="container_12">
      <div class="grid_12">
        <div id="constructor" class="constructor-block">
          <div class="cb-top-line">
            <div
              v-for="(button,index) in buttons"
              v-bind:class="['cb-step', { current: currentButton === index }]"
              v-bind:data-step="'cb-item'+index"
              v-bind:id="'cb-step'+index"
              v-on:click="currentButton=index">
              <p>
                <span>{{index+1}}</span>
                {{button}}
              </p>
            </div>
          </div>
          <div class="cb-result">
            <div class="cb-result__title">
              <p>Ваша картина</p>
            </div>
            <div class="cb-result__content">
              <p class="cb-result__data">
                <span>Изображение:</span>
                <strong></strong>
                <strong :pictureitem="pictureitem">{{pictureitem.itemname}}</strong>
              </p>
              <p class="cb-result__data">
                <span>Рама:</span>
                <strong></strong>
                <strong :borderitem="borderitem">{{borderitem.itemname}}</strong>
              </p>
              <div class="cb-result__data">
                <span>Отпечатки:</span>
                <strong>
                  <div :changemarks="changemarks"
                       v-if="changemarks == ''">Не выбрано</div>
                  <div v-else
                       :changemarks="changemarks"
                       :marks="marks"
                       v-for="chanchemark in changemarks"
                       v-bind:title="chanchemark.name"
                       v-bind:class="'marks_item'"
                       v-bind:style="{ background: chanchemark.color }"></div>
                </strong>

              </div>
              <div class="cb-result__object">
                <div class="cb-result__img">
                  <img :pictureitem="pictureitem" v-if="pictureitem.itemlink !=''" v-bind:src="pictureitem.itemlink"  width="176" height="220">
                  <img :pictureitem="pictureitem" v-else="pictureitem.itemlink !=''" v-bind:style="{ display: 'none'}" v-bind:src="pictureitem.itemlink"  width="176" height="220">
                </div>
                <div class="cb-result__border">
                  <img :borderitem="borderitem" v-bind:src="borderitem.itemlink" v-if="borderitem.itemlink !=''"  width="176" height="220">
                  <img :borderitem="borderitem" v-bind:src="borderitem.itemlink" v-else="borderitem.itemlink !=''" v-bind:style="{ display: 'none'}"   width="176" height="220">
                </div>
                <p :picturetext="picturetext" :picturefont="picturefont" v-bind:class="['cb-result__text__title', picturefont.font.toLowerCase()]">{{picturetext.title}}</p>
                <p :picturetext="picturetext" :picturefont="picturefont" v-bind:class="['cb-result__text__name', picturefont.font.toLowerCase()]">{{picturetext.name}}</p>
                <p :picturetext="picturetext" :picturefont="picturefont" v-bind:class="['cb-result__text__date', picturefont.font.toLowerCase()]">{{picturetext.date}}</p>
              </div>
            </div>
            <div class="cb-result__bottom">
              <form action="" method="POST">
                <p class="cb-next" :calk="calk" v-if="calk<3"  v-on:click="currentButton=currentButton+1" >Далее</p>
                <p class="cb-next" :calk="calk" :sendData="sendData" v-else @click="readysendData">В КОРЗИНУ</p>
                <input name="result" id="" type="text" hidden="">
              </form>
            </div>
          </div>
          <div class="cb-wrapper">
            <div id="cb-items" class="cb-item1">
              <component
                v-bind:is="currentComponent"

                :pictures="pictures"
                :borders="borders"
                :picturetext="picturetext"
                :marks="marks"
                :fonts="fonts"
                :changemarks="changemarks"
                class="current-cb-item"
                @take-pict="takepict"
                @take-border="takebord"
                v-on:change-txt="chantext"
                v-on:change-font="changefont"
                v-on:change-mark="chagemarks"
              ></component>
            </div>
          </div>
          <div class="cb-bottom-line">
            <div class="cb-total">
              <span class="cb-total__text">Стоимость:</span><span class="cb-total__amount" :changemarks="changemarks"
                                                                  v-if="changemarks.length<3"> 550</span>
              <span class="cb-total__amount" :changemarks="changemarks"
                    v-else>{{changemarks.length*10 + 550}}</span>
              <span class="cb-total__currency"> грн</span>

            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import CbItem0 from './CbItem0.vue';
  import CbItem1 from './CbItem1.vue';
  import CbItem2 from './CbItem2.vue';
  import CbItem3 from './CbItem3.vue';
export default {
  data () {
    return {
      currentButton: 0,
      buttons:['Изображение','Рама','Заголовок','Цвет отпечатков'],
      pictures:[
        {
          number: '01',
          name: 'Картинка №1',
          imageLink: 'src/assets/img/pics/01.jpg'
        },
        {
          number: '02',
          name: 'Картинка №2',
          imageLink: 'src/assets/img/pics/02.jpg'
        },
        {
          number: '03',
          name: 'Картинка №3',
          imageLink: 'src/assets/img/pics/03.jpg'
        },
        {
          number: '04',
          name: 'Картинка №4',
          imageLink: 'src/assets/img/pics/04.jpg'
        },
        {
          number: '05',
          name: 'Картинка №5',
          imageLink: 'src/assets/img/pics/05.jpg'
        },
        {
          number: '06',
          name: 'Картинка №6',
          imageLink: 'src/assets/img/pics/06.jpg'
        },
        {
          number: '07',
          name: 'Картинка №7',
          imageLink: 'src/assets/img/pics/07.jpg'
        },
        {
          number: '08',
          name: 'Картинка №8',
          imageLink: 'src/assets/img/pics/08.jpg'
        },
        {
          number: '09',
          name: 'Картинка №9',
          imageLink: 'src/assets/img/pics/09.jpg'
        },
        {
          number: '10',
          name: 'Картинка №10',
          imageLink: 'src/assets/img/pics/10.jpg'
        },
        {
          number: '11',
          name: 'Картинка №11',
          imageLink: 'src/assets/img/pics/11.jpg'
        }
      ],
      borders:[
        {
          number:'01',
          name:'Багетная №1',
          imageLink:'src/assets/img/borders/rama-01.png'
        },
        {
          number:'02',
          name:'Багетная №2',
          imageLink:'src/assets/img/borders/rama-02.png'
        },
        {
          number:'03',
          name:'Багетная №3',
          imageLink:'src/assets/img/borders/rama-03.png'
        },
        {
          number:'04',
          name:'Багетная №4',
          imageLink:'src/assets/img/borders/rama-04.png'
        },
        {
          number:'05',
          name:'Багетная №5',
          imageLink:'src/assets/img/borders/rama-05.png'
        },
        {
          number:'06',
          name:'Багетная №6',
          imageLink:'src/assets/img/borders/rama-06.png'
        },
        {
          number:'07',
          name:'Багетная №7',
          imageLink:'src/assets/img/borders/rama-07.png'
        },
        {
          number:'08',
          name:'Багетная №8',
          imageLink:'src/assets/img/borders/rama-08.png'
        },
        {
          number:'09',
          name:'Багетная №9',
          imageLink:'src/assets/img/borders/rama-09.png'
        },
        {
          number:'10',
          name:'Багетная №10',
          imageLink:'src/assets/img/borders/rama-10.png'
        },
        {
          number:'11',
          name:'Багетная №11',
          imageLink:'src/assets/img/borders/rama-11.png'
        },
        {
          number:'12',
          name:'Багетная №12',
          imageLink:'src/assets/img/borders/rama-12.png'
        },
        {
          number:'13',
          name:'Багетная №13',
          imageLink:'src/assets/img/borders/rama-13.png'
        },
        {
          number:'14',
          name:'Багетная №14',
          imageLink:'src/assets/img/borders/rama-14.png'
        },
        {
          number:'15',
          name:'Багетная №15',
          imageLink:'src/assets/img/borders/rama-15.png'
        }
      ],
      marks:[
        {
          name:'BahamaBlue',
          id:'mark0',
          imageLink:'src/assets/img/marks/BahamaBlue.jpg',
          color: '#2456ca',
          number: 0,
          chacked:false
        },
        {
          name:'BambooLeaves',
          id:'mark1',
          imageLink:'src/assets/img/marks/BambooLeaves.jpg',
          color: '#6f8c19',
          number: 1,
          chacked:false
        },
        {
          name:'LilacPosies',
          id:'mark2',
          imageLink:'src/assets/img/marks/LilacPosies.jpg',
          color: '#aa288b',
          number: 2,
          chacked:false
        },
        {
          name:'PearTart',
          id:'mark3',
          imageLink:'src/assets/img/marks/PearTart.jpg',
          color: '#d1d22a',
          number: 3,
          chacked:false
        },
        {
          name:'RhubarbStalk',
          id:'mark4',
          imageLink:'src/assets/img/marks/RhubarbStalk.jpg',
          color: '#881f3c',
          number: 4,
          chacked:false
        },{
          name:'Tangelo',
          id:'mark5',
          imageLink:'src/assets/img/marks/Tangelo.jpg',
          color: '#f26a27',
          number: 5,
          chacked:false
        },
        {
          name:'CottageIvy',
          id:'mark6',
          imageLink:'src/assets/img/marks/CottageIvy.jpg',
          color: '#1d6b3e',
          number: 6,
          chacked:false
        },
        {
          name:'PearTart',
          id:'mark7',
          imageLink:'src/assets/img/marks/PearTart.jpg',
          color: '#e3e072',
          number: 7,
          chacked:false
        },
        {
          name:'BahamaBlue',
          id:'mark8',
          imageLink:'src/assets/img/marks/BahamaBlue.jpg',
          color: '#2456ca',
          number: 8,
          chacked:false
        },
        {
          name:'PottersClay',
          id:'mark9',
          imageLink:'src/assets/img/marks/PottersClay.jpg',
          color: '#d07a2d',
          number: 9,
          chacked:false
        }
      ],
      pictureitem: {
        itemlink:'',
        itemname: 'Не выбрано'
      },
      borderitem:{
        itemlink:'',
        itemname: 'Не выбрано'
      },
      picturetext:{
        title:'',
        name:'',
        date:'',
        font:'ariston'
      },
      picturefont:{
        font:'ariston'
      },
      fonts:['Ariston','DaVinci','Brody'],
      changemarks:[],
      calk:0,
      sendData:{
        picture:'',
        border:'',
        title:'',
        name:'',
        date:'',
        font:'',
        marks:[]
      },
      errors:[]
    }
  },
  methods:{
    takepict: function(index){
      this.pictureitem.itemlink = this.pictures[index].imageLink;
      this.pictureitem.itemname = this.pictures[index].name;
      this.sendData.picture = this.pictureitem.itemname;
      this.calk = this.calk+1;
      console.log(this.sendData.picture);
      console.log(this.calk);
    },
    takebord:function (index) {
      this.borderitem.itemlink = this.borders[index].imageLink;
      this.borderitem.itemname = this.borders[index].name;
      this.sendData.border = this.borderitem.itemname;
      this.calk = this.calk+1;
      console.log(this.calk);
    },
    chantext:function (val) {
      this.picturetext= val;
      this.sendData.title = this.picturetext.title;
      this.sendData.name = this.picturetext.name;
      this.sendData.date = this.picturetext.date;
      console.log(this.picturetext.date, this.picturetext.title, this.picturetext.name);
    },
    changefont:function (font) {
      this.picturefont.font = font;
      this.sendData.font = this.picturefont.font;
      console.log(this.picturefont.font);
    },
    chagemarks:function (index) {

      if (this.marks[index].chacked == true) {
        this.changemarks.push(this.marks[index]);
        this.sendData.marks.push(this.marks[index]);
        this.calk = this.calk+1;
      } else{
        this.changemarks.splice(this.changemarks.num,1);
        this.sendData.marks.splice(this.sendData.marks.num,1);
        this.calk = this.calk-1;
      }

      console.log(this.calk);
    },
    readysendData(){
      console.log(this.sendData.picture);
      const str = JSON.stringify(this.sendData);
      axios.post(`https://jsonplaceholder.typicode.com/posts`,str)
        .then(response=>{})
        .catch(e=>{
          this.errors.push(e);
        })
    }


  },
  computed: {
    currentComponent: function () {
      if(this.currentButton > 3){
        this.currentButton = 0;
      }
      return 'cb-item-' + this.currentButton;
    },
    readyForSent: function () {
      if(this.pictureitem.itemname != 'Не выбрано' && this.borderitem.itemname != 'Не выбрано' && this.changemarks != [] ){
        this.calk = 3;
        console.log(this.calk );
      }
    }
  },
  components:{
    CbItem0:CbItem0,
    CbItem1:CbItem1,
    CbItem2:CbItem2,
    CbItem3:CbItem3
  }
}
</script>


