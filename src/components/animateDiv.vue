<style>
.ani-container {
  perspective: 1000px;
  position: relative;
  border: solid,1px,red;
  overflow: hidden;
}

.animate-enter-active,.animate-leave-active{
  backface-visibility: hidden;
  position: absolute;
  transition: transform 0.3s linear;
}
/*占位用，最终的样式值会通过js修改*/
.animate-enter {
  transform: translateY(-30px);
}
.animate-leave-active {
  transform: translateY(30px);
}

</style>

<template>
  <div class="ani-container">
      <div v-if="trigger==='src'">
        <transition name="animate" v-on:before-enter="beforeEnter">
          <div  v-if="showFrontView"  key="front"><img :src="src" :alt="alt" :width="width" :height="height"></img></div>
          <div  v-else key="back"><img :src="src" :alt="alt" :width="width" :height="height"></img></div>
        </transition>
      </div>
      <div v-else>
        <transition name="animate" v-on:before-enter="beforeEnter">
        <div  v-if="showFrontView"  key="front">{{text}}</div>
        <div  v-else key="back">{{text}}</div>
      </transition>
      </div>
  </div>
</template>

<script>

export default{
  created:function(){
    this.rules = this.allRules();
  },
  mounted:function(){
    this.width = this.$el.clientWidth + "px";
    this.height = this.$el.clientHeight + "px";

    if (typeof this.src !== 'undefined' && this.src.length > 0) {
      this.trigger = 'src';
    }else{
      this.trigger = 'text';
    }
  },
  props:{
    animateType:{
      type:String,
      default:"drop"
    },
    text:{
      type:String,
      default:"Hello World!"
    },
    src:{
      type:String,
    },
    alt:{
      type:String,
      default:"IMG"
    },
    animateDuration:{
      type:String,
      default:"0.3s"
    },
    reverseDirection:{
      default:false
    }
  },
  data:function(){
    return {
      showFrontView:true,
      trigger:'',
      width:0,
      height:0,
      rules:{}
    }
  },
  watch:{
    text:function(newValue,oldValue){
      this.showFrontView = !this.showFrontView;
      this.trigger = "text";
    },
    src:function(newValue,oldValue){
      this.showFrontView = !this.showFrontView;
      this.trigger = "src";
    }
  },
  methods:{
    beforeEnter:function(el){
      el.style.transitionDuration = this.animateDuration;
      switch (this.animateType) {
        case "drop":{
          if (!this.reverseDirection) {
            this.getClassSheet('.animate-enter').style.transform = "translateY(-"+this.height + ")";
            this.getClassSheet('.animate-leave-active').style.transform = "translateY("+this.height + ")";
          }else{
            this.getClassSheet('.animate-enter').style.transform = "translateY("+this.height + ")";
            this.getClassSheet('.animate-leave-active').style.transform = "translateY(-"+this.height + ")";
          }
            break;
        }
        case "push":{
          if (!this.reverseDirection) {
            this.getClassSheet('.animate-enter').style.transform = "translateX(-"+this.width + ")";
            this.getClassSheet('.animate-leave-active').style.transform = "translateX("+this.width + ")";
          }else{
            this.getClassSheet('.animate-enter').style.transform = "translateX("+this.width + ")";
            this.getClassSheet('.animate-leave-active').style.transform = "translateX(-"+this.width + ")";
          }
            break;
        }
        case "flip-y":{
          if (!this.reverseDirection) {
            this.getClassSheet('.animate-enter').style.transform = "rotateY(180deg)";
            this.getClassSheet('.animate-leave-active').style.transform = "rotateY(-180deg)";
          }else{
            this.getClassSheet('.animate-enter').style.transform = "rotateY(-180deg)";
            this.getClassSheet('.animate-leave-active').style.transform = "rotateY(180deg)";
          }
          break;
        }
        case "flip-x":{
          if (!this.reverseDirection) {
            this.getClassSheet('.animate-enter').style.transform = "rotateX(180deg)";
            this.getClassSheet('.animate-leave-active').style.transform = "rotateX(-180deg)";
          }else{
            this.getClassSheet('.animate-enter').style.transform = "rotateX(-180deg)";
            this.getClassSheet('.animate-leave-active').style.transform = "rotateX(180deg)";
          }
          break;
        }
        default:
          break;
      }
    },
    beforeLeave:function(el){

    },
    enter:function(el){

    },
    allRules:function(name){
      let rules={};
      let ds=document.styleSheets,dsl=ds.length;
      console.log(ds);
      for (let i=0;i<dsl;++i){
        let dsi=ds[i].cssRules;
        let dsil=0;
        if (dsi !== null) {
          dsil = dsi.length;
        }
        for (let j=0;j<dsil;++j) rules[dsi[j].selectorText]=dsi[j];
      }
      return rules;
    },
    getClassSheet:function(name){
      if (!this.rules.hasOwnProperty(name)) {
          throw 'do not find class'+name;
      }
      return this.rules[name];
    }
  }
}
</script>
