<style lang="less">
  @import "./main.less";
</style>
<template>
  <div id="main" class="main" :class="{'main-hide-text': hideMenuText}">
    <div class="sidebar-menu-con"
         :style="{width: hideMenuText?'60px':'200px', overflow: hideMenuText ? 'visible' : 'auto', background: '#515a6e'}">
      <div class="logo-con">
      </div>
      <sidebar-menu v-if="!hideMenuText" :menuList="menuList" :iconSize="18"/>
      <sidebar-menu-shrink v-else :menuList="menuList"/>
    </div>
    <div class="main-header-con" :style="{paddingLeft: hideMenuText?'60px':'200px'}">
      <div class="main-header">
        <div class="navicon-con">
          <Button :style="{transform: 'rotateZ(' + (this.hideMenuText ? '-90' : '0') + 'deg)'}" type="text"
                  @click="toggleClick">
            <Icon type="md-menu" size="32"></Icon>
          </Button>
        </div>
        <div class="header-middle-con">
          <div class="main-breadcrumb">
            <breadcrumb-nav :currentPath="currentPath"></breadcrumb-nav>
          </div>
        </div>
        <!--<div class="header-avator-con">-->
          <!--<a @click="getc = true">捐助</a>-->
          <!--<Modal-->
          <!--v-model="getc"-->
          <!--title="捐助Yearning"-->
          <!--width="640">-->
          <!--<h3>让Yearning持续提供更好的功能与服务。</h3>-->
          <!--<br>-->
          <!--<img height="300" width="300" src="./assets/alipay.jpg"/>-->
          <!--<img height="300" width="300" src="./assets/wechat.jpg"/>-->
          <!--</Modal>-->
          <!--<a href="https://cookiey.github.io/Yearning-document/used/" target="_Blank">使用说明</a>-->
          <!--<div @click="handleFullScreen" v-if="showFullScreenBtn" class="full-screen-btn-con">-->
            <!--<Tooltip :content="isFullScreen ? '退出全屏' : '全屏'" placement="bottom">-->
              <!--<Icon :type="isFullScreen ? 'md-contract' : 'md-expand'" :size="23"></Icon>-->
            <!--</Tooltip>-->
          <!--</div>-->
          <!--<div @click="lockScreen" class="lock-screen-btn-con">-->
            <!--<Tooltip content="锁屏" placement="bottom">-->
              <!--<Icon type="md-lock" :size="20"></Icon>-->
            <!--</Tooltip>-->
          <!--</div>-->
          <!--<div class="user-dropdown-menu-con">-->
            <!--<Row type="flex" justify="end" align="middle" class="user-dropdown-innercon">-->
              <!--<Dropdown trigger="click" @on-click="handleClickUserDropdown">-->
                <!--<a href="javascript:void(0)">-->
                  <!--<span class="main-user-name">{{ userName }}</span>-->
                  <!--<Icon type="md-arrow-dropdown"/>-->
                <!--</a>-->
                <!--<DropdownMenu slot="list">-->
                  <!--<DropdownItem name="ownSpace">个人中心</DropdownItem>-->
                  <!--<DropdownItem name="loginout" divided>退出登录</DropdownItem>-->
                <!--</DropdownMenu>-->
              <!--</Dropdown>-->
              <!--<Avatar :src="avatorPath" style="background: #ffffff;margin-left: 10px;"></Avatar>-->
            <!--</Row>-->
          <!--</div>-->
        <!--</div>-->
      </div>
      <div class="tags-con">
        <tags-page-opened :pageTagsList="pageOpenedList"></tags-page-opened>
      </div>
    </div>
    <div class="single-page-con" :style="{paddingLeft: hideMenuText?'60px':'200px'}">
      <div class="single-page">
        <template
          v-if="$route.name === 'ddledit'
        || $route.name === 'dmledit'
        || $route.name === 'view-dml'
        || $route.name === 'serach-sql'
        ">
          <keep-alive>
            <router-view></router-view>
          </keep-alive>
        </template>
        <template v-else>
          <router-view></router-view>
        </template>
      </div>
    </div>
    <Modal
      v-model="statement"
      title="欢迎使用Yearning SQL审核平台"
      width="600"
      :mask-closable="false"
      :closable="false"
      :styles="{top: '20%'}"
      ok-text="同意"
      @on-ok="statementput"
    >
      <h3>关于Yearning:</h3>
      <br>
      <p>Yearning 是一款基于inception的开源SQL审核平台。设计的目的便是让DBA能够从手动审核的环境中释放出来.让sql审核更加流程化,标准化,自动化。非常欢迎大家体验并使用Yearning!</p>
      <br>
      <H3>关于二次开发的声明:</H3>
      <br>
      <p>作为一款开源平台。Yearning很希望有更多的开发者一起参与到开发中。同时也鼓励各公司根据自身业务对平台进行二次开发及定制。
        Yearning v1.3.1 采用AGPL 3.0许可证,以下为许可中相关的义务与责任。</p>
      <br>
      <p>1.未经原作者授权不得将Yearning 用于任何商业目的。包括通过网络提供任何基于yearning的商业服务。</p>
      <p>2.如果你修改了代码，需要在被修改的文件中说明。</p>
      <p>3.如二次开发并公布的情况下(内部使用不在该条款之内)，该软件必须为开源项目，不可为任何商业性质的商业软件。如需商业化必须获得原作者授权。</p>
      <p>4.本平台所有条款符合相应开源许可，请严格按照相关许可使用及开发。</p>
      <br>
      <h3>免责声明:</h3>
      <br>
      <p>由Yearning平台所产生的一切后果,Yearning作者本人不负一切责任! 请在进行安全评估及测试体验后使用。</p>
      <br>
      <h3>当然用的喜欢,就打赏下我吧 ^_^ 左上角点击捐助</h3>
      <br>
      <p>此声明不会对非超级管理员用户推送。当接受上述条款并点击同意后,此通知将不会再次出现在超级管理员页面中。</p>
    </Modal>
  </div>
</template>
<script>
  import sidebarMenu from './main_components/sidebarMenu.vue'
  import tagsPageOpened from './main_components/tagsPageOpened.vue'
  import breadcrumbNav from './main_components/breadcrumbNav.vue'
  import sidebarMenuShrink from './main_components/sidebarMenuShrink.vue'
  import axios from 'axios'
  import { mapState } from 'vuex'
  import util from './libs/util.js'

  export default {
    components: {
      sidebarMenu,
      tagsPageOpened,
      breadcrumbNav,
      sidebarMenuShrink
    },
    data () {
      return {
        spanLeft: 4,
        spanRight: 20,
        currentPageName: '',
        hideMenuText: false,
        userName: sessionStorage.getItem('user'),
        showFullScreenBtn: window.navigator.userAgent.indexOf('MSIE') < 0,
        isFullScreen: false,
        lockScreenSize: 0,
        avatorPath: 'static/avatar.png',
        getc: false,
        statement: false
      }
    },
    computed: mapState([
      'pageOpenedList',
      'currentPath',
      'menuList'
    ]),
    methods: {
      // 导航栏收缩
      toggleClick () {
        this.hideMenuText = !this.hideMenuText
      },
      // 个人中心
      handleClickUserDropdown (name) {
        if (name === 'ownSpace') {
          util.openPage(this, 'ownspace_index', '个人中心')
        } else if (name === 'loginout') {
          // 退出登录
          localStorage.clear()
          sessionStorage.clear()
          this.$router.push({
            name: 'login'
          })
        }
      },
      // 全屏
      handleFullScreen () {
        let main = document.getElementById('main')
        if (this.isFullScreen) {
          if (document.exitFullscreen) {
            document.exitFullscreen()
          } else if (document.mozCancelFullScreen) {
            document.mozCancelFullScreen()
          } else if (document.webkitCancelFullScreen) {
            document.webkitCancelFullScreen()
          } else if (document.msExitFullscreen) {
            document.msExitFullscreen()
          }
        } else {
          if (main.requestFullscreen) {
            main.requestFullscreen()
          } else if (main.mozRequestFullScreen) {
            main.mozRequestFullScreen()
          } else if (main.webkitRequestFullScreen) {
            main.webkitRequestFullScreen()
          } else if (main.msRequestFullscreen) {
            main.msRequestFullscreen()
          }
        }
      },
      // 锁屏
      lockScreen () {
        let lockScreenBack = document.getElementById('lock_screen_back')
        lockScreenBack.style.transition = 'all 3s'
        lockScreenBack.style.zIndex = 10000
        lockScreenBack.style.boxShadow = '0 0 0 ' + this.lockScreenSize + 'px #667aa6 inset'
        this.$store.commit('lock')
        sessionStorage.setItem('last_page_name', this.$route.name) // 本地存储锁屏之前打开的页面以便解锁后打开
        setTimeout(() => {
          lockScreenBack.style.transition = 'all 0s'
          this.$router.push({
            name: 'locking'
          })
        }, 800)
      },
      init () {
        // 全屏相关
        document.addEventListener('fullscreenchange', () => {
          this.isFullScreen = !this.isFullScreen
        })
        document.addEventListener('mozfullscreenchange', () => {
          this.isFullScreen = !this.isFullScreen
        })
        document.addEventListener('webkitfullscreenchange', () => {
          this.isFullScreen = !this.isFullScreen
        })
        document.addEventListener('msfullscreenchange', () => {
          this.isFullScreen = !this.isFullScreen
        })
        // 锁屏相关
        let lockScreenBack = document.getElementById('lock_screen_back')
        let x = document.body.clientWidth
        let y = document.body.clientHeight
        let r = Math.sqrt(x * x + y * y)
        let size = parseInt(r)
        this.lockScreenSize = size
        window.addEventListener('resize', () => {
          let x = document.body.clientWidth
          let y = document.body.clientHeight
          let r = Math.sqrt(x * x + y * y)
          let size = parseInt(r)
          this.lockScreenSize = size
          lockScreenBack.style.transition = 'all 0s'
          lockScreenBack.style.width = lockScreenBack.style.height = size + 'px'
        })
        lockScreenBack.style.width = lockScreenBack.style.height = size + 'px'
        // 问候信息相关
        if (!sessionStorage.getItem('hasGreet')) {
          let now = new Date()
          let hour = now.getHours()
          let greetingWord = {
            title: '',
            words: ''
          }
          let userName = sessionStorage.getItem('user')
          if (hour < 6) {
            greetingWord = {
              title: '凌晨好~' + userName,
              words: '早起的鸟儿有虫吃~'
            }
          } else if (hour >= 6 && hour < 9) {
            greetingWord = {
              title: '早上好~' + userName,
              words: '来一杯咖啡开启美好的一天~'
            }
          } else if (hour >= 9 && hour < 12) {
            greetingWord = {
              title: '上午好~' + userName,
              words: '工作要加油哦~'
            }
          } else if (hour >= 12 && hour < 14) {
            greetingWord = {
              title: '中午好~' + userName,
              words: '午饭要吃饱~'
            }
          } else if (hour >= 14 && hour < 17) {
            greetingWord = {
              title: '下午好~' + userName,
              words: '下午也要活力满满哦~'
            }
          } else if (hour >= 17 && hour < 19) {
            greetingWord = {
              title: '傍晚好~' + userName,
              words: '下班没事问候下爸妈吧~'
            }
          } else if (hour >= 19 && hour < 21) {
            greetingWord = {
              title: '晚上好~' + userName,
              words: '工作之余品一品书香吧~'
            }
          } else {
            greetingWord = {
              title: '深夜好~' + userName,
              words: '夜深了，注意休息哦~'
            }
          }
          this.$Notice.config({
            top: 130
          })
          this.$Notice.info({
            title: greetingWord.title,
            desc: greetingWord.words,
            duration: 4,
            name: 'greeting'
          })
          sessionStorage.setItem('hasGreet', 1)
        }
      },
      statementput () {
        axios.put(`${this.$config.url}/homedata/statement`)
      }
    },
    mounted () {
      this.$store.commit('Breadcrumbset', this.$route.matched[1].name)
      this.$store.state.currentPageName = this.$route.matched[1].name
      if (localStorage.getItem('pageOpenedList')) {
        this.$store.state.pageOpenedList = JSON.parse(localStorage.getItem('pageOpenedList'))
      } else {
        this.$store.state.pageOpenedList = [{
          title: '首页',
          path: '',
          name: 'home_index'
        }]
      }
      this.init()
      axios.get(`${this.$config.url}/homedata/messages`)
        .then(res => {
          if (res.data.statement !== 'pass') {
            this.statement = true
          }
        })
    },
    created () {
      // 权限菜单过滤相关
      this.$store.commit('Menulist')
      axios.defaults.headers.common['Authorization'] = sessionStorage.getItem('jwt')
    }
  }
</script>
