<template>
  <div>
    <NavBar></NavBar>
    <div class="content-app">
      <transition name="fadeInUp" mode="out-in">
        <router-view></router-view>
      </transition>
      <div class="footer">
        <p v-html="website.website_footer"></p>
        <center>
        <div class="scroll">
            <span  data-text="乾坤未定，你我皆是黑马">乾坤未定，你我皆是黑马</span>
        </div>
        </center>
      </div>
    </div>
    <BackTop></BackTop>
  </div>
</template>

<script>
  import { mapActions, mapState } from 'vuex'
  import NavBar from '@oj/components/NavBar.vue'

  export default {
    name: 'app',
    components: {
      NavBar
    },
    data () {
      return {
        version: process.env.VERSION
      }
    },
    created () {
      try {
        document.body.removeChild(document.getElementById('app-loader'))
      } catch (e) {
      }
    },
    mounted () {
      this.getWebsiteConfig()
    },
    methods: {
      ...mapActions(['getWebsiteConfig', 'changeDomTitle'])
    },
    computed: {
      ...mapState(['website'])
    },
    watch: {
      'website' () {
        this.changeDomTitle()
      },
      '$route' () {
        this.changeDomTitle()
      }
    }
  }
</script>

<style lang="less">

  * {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }

  a {
    text-decoration: none;
    background-color: transparent;
    &:active, &:hover {
      outline-width: 0;
    }
  }


  .content-app {
    margin-top: 80px;
    padding: 0 2%;
  }

  .footer {
    margin-top: 20px;
    margin-bottom: 10px;
    text-align: center;
    font-size: small;
  }

  .fadeInUp-enter-active {
    animation: fadeInUp .8s;
  }
  .scroll{
              animation:change 10s linear 0s infinite;
              position: relative;
              width: 200px;
              /* height: 50px;
              line-height: 50px;
              font-size: 30px; */
              white-space: nowrap;
              overflow: hidden;
              // border: 1px solid #ff0000;
            }
            @keyframes change{0%   {color:#8B008B;}25%{color:#ff0;}50%{color:#FF69B4;}75%{color:#cf0;}100% {color:#FF1493;}}
            .scroll span{
              display: inline-block;/*inline样式不能使用动画*/
              animation: scroll 12s linear infinite;
            }
            .scroll span:after{
              position: absolute;
              left: 100%;
              content: attr(data-text);
              margin-left: 4em;
            }
            @keyframes scroll {
              from {
                transform: translateX(0);
              }
              to {
                transform: translateX(calc(-100% - 4em)); /*总长再加上margin-left*/
              }
            }

</style>
