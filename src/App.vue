<template>
  <div>
    <div class="header">
      <div class="optionGroup">
        <span>动画方式</span>
        <select class="select" v-model="animateType">
          <option v-for="option in animationOptions">{{option}}</option>
        </select>
      </div>
      <div class="optionGroup">
        <span>动画方向</span>
        <select class="select" v-model="reverse">
          <option v-for="option in reverseOptions" v-bind:value="option.value">{{option.text}}
          </option>
        </select>
      </div>
    </div>
    <div class="content">
      <div class="egContainer">
        <p>动画文字(修改输入框试试)</p>
        <input v-model="text"></input>
        <animateDiv id="a" :text="text" animateDuration=".3s" :reverseDirection="reverse" :animateType="animateType"></animateDiv>
      </div>
      <div class="egContainer">
        <div>图片动画(切换图片试试)</div>
        <select v-model="src">
          <option v-for="option in options" v-bind:value="option.value">
            {{option.text}}
          </option>
        </select>
        <animateDiv id="b" :reverseDirection="reverse" :src="src" alt="图片" animateDuration="1.2s" :animateType="animateType"></animateDiv>
      </div>
    </div>
  </div>
</template>

<script>
   import animateDiv from './components/animateDiv.vue'

  export default {
    components: {animateDiv},
    data:function() {
      return {
        text:'Hello World!',
        src:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1488367920537&di=38975c1fabf302cc1283f8255a97f265&imgtype=0&src=http%3A%2F%2Fmvimg2.meitudata.com%2F56d2e545063391718.jpg',
        animateType:'drop',
        reverse:false,
        reverseOptions:[
          {text:"正向",value:false},
          {text:"反向",value:true}
        ],
        animationOptions:['drop','push','flip-x','flip-y'],
        options:[
          {text:'图片1',value:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1488367920537&di=38975c1fabf302cc1283f8255a97f265&imgtype=0&src=http%3A%2F%2Fmvimg2.meitudata.com%2F56d2e545063391718.jpg'},
          {text:'图片2',value:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1488367955658&di=dd76443d0355a5cf73fd0f6f5d6d0327&imgtype=0&src=http%3A%2F%2Fwww.dabaoku.com%2Fsucaidatu%2Fdongwu%2Fchongwujingling%2F593038.JPG'},
          {text:'图片3',value:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1488368009849&di=8b41bb9857d4d1f032d8f9ac8387717c&imgtype=0&src=http%3A%2F%2Fimg.article.pchome.net%2F00%2F31%2F71%2F71%2Fpic_lib%2Fwm%2F1452927.jpg'},
          {text:'图片4',value:'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1488962759&di=b973d1ff25211f6b49275eadf6ff89f1&imgtype=jpg&er=1&src=http%3A%2F%2Fimg4.duitang.com%2Fuploads%2Fitem%2F201601%2F04%2F20160104145421_Ld8fy.thumb.700_0.jpeg'},
        ],
      }
    },
    methods: {

    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  background: #eeeeee;
  top: 40px;
}
#a {
  top:20px;
  width:400px;
  height: 25px;
  text-align: center;
}
#b {
  width: 100%;
  height: 80%;
}
.header {
  margin-top: 80px;
  align-items: center;
  width: 100%;
  height: 80px;
  /*display: block;;
  justify-content: space-around;*/
}
.optionGroup {
  margin-left: 40px;
  display: inline-block;
}
.egContainer {
  position: relative;
  top:40px;
  vertical-align: top;
  display: inline-block;
  width: 40%;
  height: 400px;
  background: #eeeeee;
  border: 1px solid blue;
}
</style>
