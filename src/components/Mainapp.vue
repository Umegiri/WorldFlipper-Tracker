<template>
  <q-layout view="hHh lpR fFf">

    <q-header elevated class="bg-primary text-white" height-hint="98">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="../../public/favicon.png">
          </q-avatar>
          みんなのワーフリ
        </q-toolbar-title>
      </q-toolbar>

      <q-tabs align="center">
        <q-route-tab to="/page1" label="キャラクター" />
        <q-route-tab to="/page2" label="ウェポン" />
      </q-tabs>
    </q-header>
    <q-page-container>
      <div v-for="(item,index) in chara_data" :key="item.id" 
          :class="item" 
          class="chara shadow-20"
          @click="selectchara($event,index)">
        <img :src="require('../../public/chara/'+ index + '.png')">
      </div>
      <q-page-scroller position="bottom-right" :scroll-offset="150" :offset="[18, 18]">
        <q-btn fab icon="keyboard_arrow_up" color="accent" />
      </q-page-scroller>
      <q-dialog v-model="alert" class="detail">
      <q-card>
        <q-card-section>
          <div class="charaicon" style="font-size:30px;font-family: myFont"><img :src="require('../../public/chara/'+ selectedcharaid + '.png')">{{chara_data[selectedcharaid].name}}</div>
        </q-card-section>

        <q-card-section class="characontent">
          <q-chip square style="font-family: myFont">属性</q-chip><span style="font-family: myFont">{{chara_data[selectedcharaid].element}}</span><br>
          <q-chip square style="font-family: myFont">队长技能</q-chip><span style="font-family: myFont">{{chara_data[selectedcharaid].leader}}</span><br>
          <q-chip square style="font-family: myFont">必杀技</q-chip><span style="font-family: myFont">{{chara_data[selectedcharaid].skill}}</span><br>
          <q-chip outline color="primary" text-color="white" style="font-family: myFont">能力1</q-chip><span style="font-family: myFont">{{chara_data[selectedcharaid].ability[0]}}</span><br>
          <q-chip outline color="primary" text-color="white" style="font-family: myFont">能力2</q-chip><span style="font-family: myFont">{{chara_data[selectedcharaid].ability[1]}}</span><br>
          <q-chip outline color="primary" text-color="white" style="font-family: myFont">能力3</q-chip><span style="font-family: myFont">{{chara_data[selectedcharaid].ability[2]}}</span><br>
          <q-chip outline color="primary" text-color="white" style="font-family: myFont">能力4</q-chip><span style="font-family: myFont">{{chara_data[selectedcharaid].ability[3]}}</span><br>
          <q-chip outline color="primary" text-color="white" style="font-family: myFont">能力5</q-chip><span style="font-family: myFont">{{chara_data[selectedcharaid].ability[4]}}</span><br>
          <q-chip outline color="primary" text-color="white" style="font-family: myFont">能力6</q-chip><span style="font-family: myFont">{{chara_data[selectedcharaid].ability[5]}}</span>
        </q-card-section>

      </q-card>
    </q-dialog>
    </q-page-container>

  </q-layout>
</template>

<script>
import chara_data from '../assets/res.json'
import { Loading } from 'quasar'

export default {
    name:'Mainapp',
  data () {
    return {
      alert:false,
      chara_data,
      selectedcharaid:'',
      isloaded:false
    }
  },
  mounted(){
    this.showLoading()
  },
  methods:{
    selectchara($event,index){
      this.alert = true;
      //console.log(index);
      this.selectedcharaid = index
      //console.log(this.selectedcharaid);
    },
    showLoading(){
      if(this.isloaded === false){Loading.show({message:'页面数据加载中...'})}
      else{window.clearInterval(this.timer)}
      const timer = setInterval(() => {
        if(document.readyState === 'complete'){
          this.isloaded = true
          Loading.hide()
        }
      }, 20);
    }
  }
}
</script>

<style>
  .q-layout{
    font-family: myFont;
  }
  @font-face {
    font-family: myFont;
    src: url(../../public/font.ttf);
  }
  .chara{
    width: 82px;
    margin-top:20px;
    margin-left: 30px;
    text-align: center;
    justify-content: center;
    display: inline-flex;
  }
  .chara :hover{
    -webkit-animation: shadow-drop-2-center 0.2s both;
	          animation: shadow-drop-2-center 0.2s both;
  }
  .q-page-container{
    background-image: url('../../public/bg.png');
    margin:0 auto;
  }
  @-webkit-keyframes shadow-drop-2-center {
  0% {
    -webkit-transform: translateZ(0);
            transform: translateZ(0);
    -webkit-box-shadow: 0 0 0 0 rgba(0, 0, 0, 0);
            box-shadow: 0 0 0 0 rgba(0, 0, 0, 0);
  }
  100% {
    -webkit-transform: translateZ(50px);
            transform: translateZ(50px);
    -webkit-box-shadow: 0 0 20px 0px rgba(240, 40, 100, 0.35);
            box-shadow: 0 0 20px 0px rgba(240, 40, 100, 0.35);
  }
}
@keyframes shadow-drop-2-center {
  0% {
    -webkit-transform: translateZ(0);
            transform: translateZ(0);
    -webkit-box-shadow: 0 0 0 0 rgba(0, 0, 0, 0);
            box-shadow: 0 0 0 0 rgba(0, 0, 0, 0);
  }
  100% {
    -webkit-transform: translateZ(50px);
            transform: translateZ(50px);
    -webkit-box-shadow: 0 0 20px 10px rgba(240, 40, 100, 0.35);
            box-shadow: 0 0 20px 10px rgba(240, 40, 100, 0.35);
  }
}
</style>