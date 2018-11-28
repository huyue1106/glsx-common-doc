<template>
  <div id="app">
    <gl-header :height='"100px"'>
      <div>
        <div class="img"><img src="./assets/logo.png"></div>
        <h1><span>glsx-vue-common使用文档</span></h1>
      </div>
    </gl-header>
    <div class="app-main">
    <gl-container style="margin-top: 100px;">
      <gl-aside class="aside" :width='"350px"'>
        <ul class="pure-menu-list">
          <li><a href="#" id="introduction" ref="introduction" @click="addActive('introduction')">介绍</a></li>
          <li><a href="#instructions" id="ins" ref="ins" @click="addActive('ins')">使用方法</a></li>
          <li><a href="#introductionMethod" ref="intMethod" id="intMethod" @click="addActive('intMethod')">方法介绍</a></li>
          <ul class="fun" v-for="(k, ind) in prototypesList" :key="ind">
            <li><a :href="'#' + k.id" :id="k.method" ref="active" @click="addActive(ind)">{{k.method}}</a></li>
          </ul>
          <li><a href="#introKey" id="introductionKey" ref="introductionKey" @click="addActive('introductionKey')">介绍Key</a></li>
          <li><a href="#needLead" id="needLeadKey" ref="needLeadKey" @click="addActive('needLeadKey')">按需引入</a></li>
          <li><a href="#KeyTable" id="tableKey" ref="tableKey" @click="addActive('tableKey')">Key表</a></li>
          <!-- <ul class="fun" v-for="(index, item) in constsList" :key="item + firstKeyLen">
            <li><a :href="'#' + index.id" :id="index.Key" ref="active" @click="addActive(item + firstKeyLen)">{{index.Key}}</a></li>
          </ul> -->
        </ul>
      </gl-aside>
        <gl-main class="main">
          <h2>介绍</h2>
          <p id="instructions">glsx-vue-common为广联运营支撑平台提供了一套通用方法。</p>
          <br><br>
          <h2>使用方法</h2>
          <h4>安装</h4>
          <pre><code class="hljs">$ npm i glsx-vue-common@latest</code></pre>
          <h4>引入</h4>
          <p><code>GlsxVueCommon</code>模块通过下面的方式引入</p>
          <pre><code class="hljs">import GlsxVueCommon from 'glsx-vue-common'
Vue.use(GlsxVueCommon, common.data)  //common.data是配置文件中数据</code></pre>
          <small class="tips">注意：配置文件存放在<a class="blue" href="http://192.168.3.171:7300/project/5be17454f31545347559d499" target="blank">这里</a></small>
          <p id="introductionMethod"><code>GlAxios</code>，<code>GlConst</code>，<code>GlValidate</code>，<code>GlCommon</code>等模块通过下面的方式引入（根据需要的模块进行引入）</p>
            <pre><code class="hljs">import { GlAxios, GlConst, GlValidate, GlCommon } from 'glsx-vue-common'</code></pre>
          <br>
          <h2>方法介绍</h2>
          <small>注：Key可以自行设置，也可使用已有的Key</small>
          <div v-for="(k, ind) in prototypesList" :key="ind">
            <a href="" :id="k.id"><br><br><br><br></a>
            <h3>{{k.method}}</h3>
            <ul>
              <li><p><strong>参数：</strong><code class="params">{{k.parameter}}</code></p></li>
              <li><p><strong>描述：</strong><code>{{k.description}}</code></p></li>
              <li><p><strong>使用说明：</strong><code>{{k.instructions}}</code></p></li>
              <small class="tips">{{k.tips}}</small>
            </ul>
          </div>
          <a href="" id="introKey"><br><br><br><br></a>
          <h2>介绍Key</h2>
          <p id="needLead">所有数据都是以键值对的形式存储使用，Key就是它们的键，value是值</p>
          <br><br>
          <h2>按需引入</h2>
          <p id="KeyTable">当需要引用common中设置的Key，请根据需要引入下面的代码</p>
          <pre><code class="hljs">import { GlConst } from 'glsx-vue-common'
    const { AppConst, AsideConst, HeaderConst, FooterConst } = GlConst</code></pre>
          <h2>Key表</h2>
          <small>注：前六个未暴露，common外不可使用</small>
          <!-- <div v-for="(index, item) in constsList" :key="item+firstKeyLen">
            <a href="" :id="index.id"><br><br><br><br></a>
            <h3>{{index.Key}}</h3>
            <ul>
              <li><p><strong>Key：</strong><code class="params">{{index.Key}}</code></p></li>
              <li><p><strong>描述：</strong><code>{{index.description}}</code></p></li>
            </ul>
          </div> -->
          <consts style="margin-top: 30px;"></consts>
        </gl-main>
    </gl-container>
    </div>
    <gl-footer ref="top">Copyright © 2012-2022 深圳广联赛讯有限公司 版权所有</gl-footer>
  </div>
</template>

<script>
import consts from './components/consts'
export default {
  name: 'App',
  components: {
    consts
  },
  data () {
    return {
      prototypesList: [],
      constsList: [],
      oldActive: ''
      // firstKeyLen: ''
    }
  },
  mounted () {
    this.$http.get('../../static/data.json').then(res => {
      this.prototypesList = res.body.data
      // this.firstKeyLen = this.prototypesList.length
      this.constsList = res.body.consts
    })
  },
  methods: {
    addActive (index) {
      if (typeof (index) === 'number') {
        this.oldActive && this.$refs[this.oldActive].removeAttribute('style')
        this.$refs.active.forEach(element => {
          element.removeAttribute('style')
        })
        this.$refs.active[index].setAttribute('style', 'color: #409eff')
      } else {
        this.oldActive && this.$refs[this.oldActive].removeAttribute('style')
        this.$refs[index].setAttribute('style', 'color: #409eff')
        this.oldActive = JSON.parse(JSON.stringify(index))
      }
    }
  }
}
</script>

<style>
</style>
