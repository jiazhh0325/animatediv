# animatediv

> A animate div components for Vue2.x. Worked with Vue's v-bind automatically. Supported animation includes 'drop','push','flip-x' and 'flip-y'.

##Usage

> Import animateDiv:
```
import animateDiv from './components/animateDiv.vue'
components: {animateDiv},

```
> in template:
```
<animateDiv id="a" :text="text" :reverseDirection="reverse" :animateType="animateType"></animateDiv>
<animateDiv id="b" :reverseDirection="reverse" :src="src" alt="图片" animateDuration="1.2s" :animateType="animateType"></animateDiv>
```

##Notes
> animateDiv's size should be configed first. otherwise the 'push' & 'drop' animation will not work!!!

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
