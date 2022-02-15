<style scoped lang="scss">

  $maxWidthMainPx: 1280px;
  $maxWidthMain2Px: 965px;

  #v-app-page
  {
    background: var(--kr-color-main-white);
  }

  #v-header-wrapper
  {
    position: absolute;
    max-width: $maxWidthMainPx;
    min-width: 320px;
    width: 100%;
    display: inline-block;

    top: 0;
    left: 50%;

    transform: translateX(-50%);
  }

  #v-body
  {
    width: 100%;
    display: inline-block;
    margin-top: 96px;
    transition: margin-top 300ms ease-in-out, opacity 0.5s ease, transform 0.5s ease;

    min-height: calc(100vh - 96px);
  }

  #v-footer
  {
    max-width: $maxWidthMainPx;
    min-width: 320px;
    width: 100%;
    display: inline-block;
  }

  #v-app-scrollbar
  {
    position: fixed;
    height: 100vh;
    z-index: 99999;
  }

  .fade-enter-active,
  .fade-leave-active
  {
    transition: opacity .3s cubic-bezier(0.36, 0.83, 0.48, 0.99);

  }

  .fade-enter-from,
  .fade-leave-to
  {
    opacity: 0;
  }

  @media (max-width: 1280px)
  {
    #v-header-wrapper
    {
      max-width: $maxWidthMain2Px;
    }
  }

  @media (max-width: 945px)
  {
    #v-body
    {
      margin-top: 80px;
      min-height: calc(100vh - 80px);
    }
  }

  @media (max-width: 440px)
  {
    #v-body
    {
      margin-top: 64px;
      min-height: calc(100vh - 64px);
    }
  }
</style>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

  @import "./stylesheets/fonts";
  @import "./stylesheets/colors";

  $maxWidthMainPx: 1280px;
  $maxWidthMain2Px: 944px;

  @mixin focus-style{
    box-shadow: 0 0 0 3px rgba(0, 128, 255, 0.16);
  }

  html, body
  {
    -ms-overflow-style: none; /* Internet Explorer 10+ */
    scrollbar-width: none; /* Firefox */

    &::-webkit-scrollbar {
      display: none; /* Safari and Chrome */
    }
  }

  body {
    margin: 0;

    -webkit-tap-highlight-color: transparent;

    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;

    position: relative;
  }

  .always-display-focus
  {
    &:focus
    {
      @include focus-style;
    }
  }

  :focus
  {
    outline: none;
  }

  .as-keyboarduser
  {
    :focus
    {
      @include focus-style;
    }
  }

  .kr-body
  {
    max-width: $maxWidthMainPx;
    min-width: 320px;
    width: 100%;
    display: inline-block;
  }

  .kr-body-margin-top
  {
    margin-top: 56px;
  }

  .kr-body-margin-bottom
  {
    margin-bottom: 56px;
  }

  @media (max-width: 1280px)
  {
    .kr-body
    {
      max-width: $maxWidthMain2Px;
    }
  }

  @media (max-width: 640px)
  {
    .kr-body-margin-bottom
    {
      margin-bottom: 40px;
    }
  }

  @media (max-width: 945px)
  {
    .kr-body-margin-top
    {
      margin-top: 40px;
    }
  }

  @media (max-width: 440px)
  {
    .kr-body-margin-top
    {
      margin-top: 24px;
    }
  }
</style>

<template>
  <!--<scrollbar-component
          id="v-app-page"
          @click="clicked"
          @keydown="pressedKeyboard"
          :class="{ 'as-keyboarduser': !isMouseUser }"


          :lock="openedMenu"
          scroll-name="body"
          :screen-mode="true"
  >-->
  <screen-component id="v-app-page"
                    @click="clicked"
                    @keydown="pressedKeyboard"
                    :class="{ 'as-keyboarduser': !isMouseUser }"

                    :lock="openedMenu"
  >
    <div id="v-body">
      <router-view v-slot="{ Component }">
        <transition :name=" disableTransition ? 'fadedis' : 'fade'"
                    mode="out-in"

                    @before-enter="beforeEnterPageTransition"
                    @enter="enterPageTransition"
                    @after-enter="afterEnterPageTransition"
                    @enter-cancelled="enterCancelledPageTransition"

                    @before-leave="beforeLeavePageTransition"
                    @leave="leavePageTransition"
                    @after-leave="afterLeavePageTransition"
        >
          <component v-if="isDisplayedPage" :is="Component" />
          <loading v-else />
        </transition>
      </router-view>
    </div>
    <div id="v-footer" ref="footer">
      <footer-component />
    </div>
    <div id="v-header-back"></div>
    <div id="v-header-wrapper" ref="header">
      <header-component @opened-menu="onOpenMenu" @closed-menu="onCloseMenu" />
    </div>
  </screen-component>
  <scrollbar-component id="v-app-scrollbar" :scroll-element="bodyElement" />
</template>

<script>
  import { Options, Vue } from "vue-class-component";

  import HeaderComponent from './components/HeaderComponent';
  import FooterComponent from "./components/FooterComponent";
  import Loading from "./views/Loading";

  import ScrollbarComponent from "./components/base/ScrollbarComponent";
  import ScreenComponent from "@/components/base/ScreenComponent";

  let popStateDetected = false;
  window.addEventListener('popstate', () => {
    popStateDetected = true;
  });

  let pageFirstLoaded = true;

  const Component = Options;
  @Component({
    components: {
      ScreenComponent,
      HeaderComponent,
      FooterComponent,
      Loading,
      ScrollbarComponent
    },
    props: {

    }
  })
  export default class App extends Vue {
    isMouseUser = true;

    isDisplayedPage = false;

    disableTransition = false;

    prevPageDissapear = false;
    smoothDisplayHeader = false;

    openedMenu = false;

    bodyElement = document.documentElement;

    onOpenMenu()
    {
      window.scrollTo({
        top: 0
      });
      this.openedMenu = true;
    }

    onCloseMenu()
    {
      this.openedMenu = false;
    }

    beforeEnterPageTransition()
    {
      this.$refs.footer.classList.add('fade-enter-from');
    }

    enterPageTransition()
    {
      const _this = this;
      setTimeout(() => {
        _this.$refs.footer.classList.add('fade-enter-active');
        _this.$refs.footer.classList.remove('fade-enter-from');
      }, 1);

      if(this.smoothDisplayHeader)
      {
        setTimeout(() => {
          _this.$refs.header.classList.add('fade-enter-active');
          _this.$refs.header.classList.remove('fade-enter-from');
        }, 1);
      }
    }

    afterEnterPageTransition()
    {
      this.$refs.footer.classList.remove('fade-enter-active');

      if(this.smoothDisplayHeader)
      {
        this.$refs.header.classList.remove('fade-enter-active');
        this.smoothDisplayHeader = false;
      }
    }

    enterCancelledPageTransition()
    {
      this.afterEnterPageTransition();
    }

    beforeLeavePageTransition()
    {

    }

    leavePageTransition()
    {
      const _this = this;
      setTimeout(() => {
        _this.$refs.footer.classList.add('fade-leave-active', 'fade-leave-to');
      }, 1);
    }

    afterLeavePageTransition()
    {
      this.$refs.footer.classList.remove('fade-leave-active', 'fade-leave-to');

      if(this.prevPageDissapear)
      {
        const rectHeader = this.$refs.header.getBoundingClientRect();
        if(rectHeader.top + rectHeader.height < 0)
        {
          window.scrollTo({
            top: 0
          });
          this.$refs.header.classList.add('fade-enter-from');
          this.smoothDisplayHeader = true;
        }

        this.prevPageDissapear = false;
      }
    }

    created()
    {
      const _this = this;
      routerGlobal.beforeEach((to, from, next) => {
        if(pageFirstLoaded)
        {
          pageFirstLoaded = false;
        }
        else
        {
          if(!popStateDetected)
          {
            _this.prevPageDissapear = true;
            _this.isDisplayedPage = false;
            _this.disableTransition = false;
          }
          else
          {
            _this.disableTransition = true;
            popStateDetected = false;
          }
        }

        next();
      });

      routerGlobal.afterEach((to, from) => {
        this.isDisplayedPage = true;
      });

      if(navigator.platform.indexOf("iPhone") > -1 || navigator.platform.indexOf("iPad") > -1 ||
              navigator.platform.indexOf("iPod") > -1)
      {
        document.body.classList.add("kr-ios");
        document.body.classList.add("kr-mobile");
      }

      if(navigator.platform.indexOf("Android") > -1)
      {
        document.body.classList.add("kr-android");
        document.body.classList.add("kr-mobile");
      }
    }

    clicked()
    {
      this.isMouseUser = true;
    }

    pressedKeyboard(event)
    {
      this.isMouseUser = false;
    }
  }
</script>