<style scoped lang="scss">
    @import "../stylesheets/kira-fonts";

  .v-background-city
  {
        $maxHeight: 264;
        $minHeight440px: 104;

        position: relative;
        width: 100%;
        height: calc(#{$maxHeight}px - ((1920px - 100vw) /
                    #{(1920 - 440)}) * #{$maxHeight - $minHeight440px});

        background: #F0FFE9;
  }

  .v-background-circle
  {
    position: absolute;
    display: block;
    width: 100%;
    top: 0;
    left: 0;
  }

  .v-background-city-svg
  {
    left: 0;
    bottom: 0;

    transform: translateX(0%);

    position: absolute;
    width: 100%;
    //height: 140px;
    background: url("../assets/CityPattern.svg");
    background-position-x: calc(50%);

      $maxBgSize: 850;
      $minBgSize440px: 553;

      $maxHeight: 138;
      $minHeight440px: 90;

      background-size: calc(#{$maxBgSize}px - ((1920px - 100vw) /
                            #{(1920 - 440)}) * #{$maxBgSize - $minBgSize440px});
      height: calc(#{$maxHeight}px - ((1920px - 100vw) /
                    #{(1920 - 440)}) * #{$maxHeight - $minHeight440px});
  }

    .v-welcome-block
    {
        width: 100%;

        text-align: left;

        .v-title
        {
            display: inline-flex;

            margin-left: 92px;
            color: var(--kr-color-main-plain-text);
            text-align: left;

            @include kiraFont(h1);
        }

        .v-group
        {
            margin-top: 48px;
            margin-left: 92px;

            display: inline-block;

            .v-text
            {
                color: var(--kr-color-main-plain-text);

                text-align: left;

                width: 316px;
                height: 64px;

                display: inline-block;

                @include kiraFont(body-1);

                &:not(:last-child)
                {
                    margin-right: 48px;
                }
            }
        }
    }

    .v-loader-box
    {
        width: 100px;
        height: 100px;
    }

    .v-news
    {
        margin-top: 40px;
    }

    .v-arts
    {
        margin-top: 32px;
    }

  @media (max-width: 1280px)
  {
      .v-welcome-block
      {
          .v-title
          {
              margin-left: 132px;
          }

          .v-group
          {
              margin-top: 32px;
              margin-left: 132px;

              width: 730px;

              .v-text
              {
                  &:not(:last-child)
                  {
                      margin-bottom: 24px;
                  }
              }
          }
      }
  }

  @media (max-width: 945px)
  {
      .v-news
      {
          margin-top: 24px;
      }

      .v-welcome-block
      {
          text-align: center;
          margin-left: 0;

          .v-title
          {
              margin-left: 0;

              @include kiraFont(h2);
          }

          .v-group
          {
              width: 100%;
              margin-left: 0;
              text-align: center;

              .v-text
              {
                  &:not(:last-child)
                  {
                      margin-right: 0;
                  }

                  position: relative;

                  display: flex;

                  margin-left: 0;
                  margin-right: 0;

                  left: 50%;
                  transform: translateX(-50%);

                  text-align: center;
              }
          }
      }
  }

  @media (max-width: 490px)
  {
      .v-block-title
      {
          margin-left: 20px;
      }

      .v-news
      {
          margin-top: 32px;
      }

      .v-welcome-block
      {
          .v-title
          {
              @include kiraFont(h3);
          }

          .v-group
          {
              margin-top: 16px;

              .v-text
              {
                  width: 256px;
                  height: 48px;

                  @include kiraFont(body-2);
              }
          }
      }

  }
</style>

<template>
    <div>
        <div class="kr-body kr-body-margin-top">
            <div class="v-welcome-block">
                <div class="v-title">ТСЖ «Фортуна»</div>
                <div class="v-group">
                    <div class="v-text">Актуальная информация о работе нашего ТСЖ</div>
                    <div class="v-text">Важные объявления и новости для жильцов</div>
                    <div class="v-text">Протоколы и бухгалтерская отчетность</div>
                </div>
            </div>
        </div>

        <div class="v-background-city">
            <svg class="v-background-circle" viewBox="0 0 1920 144" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M960 144C269.251 144 0 0 0 0H1920C1920 0 1650.75 144 960 144Z" fill="white"/>
            </svg>

            <div class="v-background-city-svg"></div>
        </div>

        <div class="kr-body kr-body-margin-bottom">
            <div class="v-news">
                <news-preview-block-component />
            </div>
            <div class="v-arts">
                <arts-preview-block-component/>
            </div>
        </div>
    </div>
</template>

<script>
  import { Options, Vue } from "vue-class-component";

  import LoaderBoxComponent from '../components/LoaderBoxComponent';
  import NewsPreviewBlockComponent from '../components/NewsPreviewBlockComponent';
  import ArtsPreviewBlockComponent from '../components/ArtsPreviewBlockComponent';

  const Component = Options;
  @Component({
    components: {
        LoaderBoxComponent,
        NewsPreviewBlockComponent,
        ArtsPreviewBlockComponent
    },
    props: {

    }
  })
  export default class Home extends Vue {
      isMouseUser = true;

      mounted()
      {
          document.title = "ТСЖ «Фортуна» – Официальный сайт Управляющей Компании в г. Хабаровск";
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