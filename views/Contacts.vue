<style scoped lang="scss">
  @import '../stylesheets/kira-fonts';

  .kr-body
  {
    text-align: left;

    h1
    {
      @include kiraFont(h1);
    }

    h3
    {
      @include kiraFont(h3);
    }

    h1,h3
    {
      color: var(--kr-color-layout-black-metallic);

      margin-top: 0;
      margin-bottom: 24px;
    }
  }

  .v-yandex-map-block
  {
    display: inline-block;
    vertical-align: top;
  }

  .v-yandex-map
  {
    display: inline-block;
    width: 427px;
    height: 427px;

    vertical-align: top;

    .v-box
    {
      width: 100%;
      height: 100%;
    }
  }

  .v-contacts-info-block
  {
    display: inline-block;
    vertical-align: top;
    margin-left: 48px;
  }

  .v-contacts
  {
    margin-bottom: 48px;
  }

  .v-contact
  {
    display: inline-block;

    &:not(:last-child)
    {
      margin-right: 24px;
    }

    .v-title
    {
      color: var(--kr-color-main-help-text);
      margin-bottom: 4px;
    }
  }

  .v-contact-f-column
  {
    vertical-align: top;
    display: inline-block;
    width: 282px;

    &:not(:last-child)
    {
      margin-right: 48px;
    }

    &.v-contact-f-column-2
    {
      width: 320px;
    }
  }

  .v-mode-work-block
  {
    display: inline-block;

    margin-bottom: 24px;
  }

  .v-mode-work
  {
    &:not(:last-child)
    {
      margin-bottom: 48px;
    }

    .v-title
    {
      color: var(--kr-color-main-header);
      margin-bottom: 8px;
    }

    .v-text
    {
      color: var(--kr-color-main-plain-text);
    }
  }

  .v-useful-phones
  {
    margin-top: 48px;
  }


  .v-address-block
  {
    display: inline-block;

    &:not(:last-child)
    {
      margin-right: 24px;
    }

    .v-title
    {
      margin-bottom: 8px;
    }

    .v-main-title
    {
      display: inline-block;
      margin-right: 8px;

      color: var(--kr-color-main-header);
    }

    .v-sub-title
    {
      display: inline-block;
      margin-top: 4px;

      color: var(--kr-color-main-help-text);
    }

    .v-address
    {
      color: var(--kr-color-main-help-text);
      margin-bottom: 4px;
    }
  }

  @media (max-width: 1280px)
  {
    .v-contacts-info-block
    {
      width: 477px;
      margin-left: 40px;
    }

    .v-contact
    {
      &:not(:last-child)
      {
        margin-bottom: 24px;
      }
    }

    .v-useful-phones
    {
      width: 427px;
    }

    .v-address-block
    {
      &:not(:last-child)
      {
        margin-bottom: 24px;
      }
    }

    .v-contact-f-column
    {
      &:not(:last-child)
      {
        margin-bottom: 40px;
      }

      width: auto;

      &.v-contact-f-column-2
      {
        width: auto;
      }
    }
  }

  @media (max-width: 1024px)
  {
    .kr-body
    {
      width: 560px;
    }

    .v-yandex-map
    {
      margin-top: 8px;
      width: 560px;
      height: 560px;
    }

    .v-contacts-info-block
    {
      width: unset;
      margin-left: 0;
    }

    .v-useful-phones
    {
      width: unset;
      margin-top: 32px;
    }

    .v-contacts
    {
      margin-bottom: 16px;
    }

    .v-mode-work
    {
      &:not(:last-child)
      {
        margin-bottom: 32px;
      }
    }

    .v-contact-f-column
    {
      &:not(:last-child)
      {
        margin-bottom: 32px;
      }
    }

    .v-address-block
    {
      margin-bottom: 24px;
    }
  }

  @media (max-width: 640px) {
      .kr-body
      {
        width: calc(100vw - 40px);
        margin-left: 20px;
        margin-right: 20px;
        min-width: 0;

        h1
        {
          @include kiraFont(h3);
        }

        h3
        {
          margin-bottom: 16px;
        }
      }

    .v-yandex-map-block
    {
      display: block;
    }

    .v-contacts
    {
      margin-bottom: 8px;
    }

    .v-contact
    {
      margin-right: 16px;
      margin-bottom: 16px;

      &:not(:last-child)
      {
        margin-right: 16px;
      }
    }

    .v-address-block
    {
      margin-right: 16px;
      &:not(:last-child)
      {
        margin-right: 16px;
      }
    }

    .v-mode-work-block
    {
      display: block;
      margin-bottom: 16px;
    }

    .v-mode-work
    {
      &:not(:last-child)
      {
        margin-bottom: 24px;
      }
    }

    .v-yandex-map
    {
      width: calc(100vw - 40px);
      height: calc(100vw - 40px);
    }

    .v-contact-f-column
    {
      &:not(:last-child)
      {
        margin-bottom: 24px;
        margin-right: 0;
      }

      margin-right: 0;
    }


    .v-useful-phones
    {
      margin-top: 24px;
    }

  }
</style>

<template>
  <div ref="main_body" class="kr-body kr-body-margin-top kr-body-margin-bottom">
    <h1>Контакты</h1>
    <div class="v-yandex-map-block" ref="yandex_map_block">
      <div class="v-yandex-map" ref="yandex_map">
        <loader-box-component v-if="!isLoadedMap" class="v-box"/>
      </div>
    </div>

    <div class="v-contacts-info-block">
      <div class="v-contacts">
        <div class="v-contact">
          <div class="v-title kr-font-body-2">Председатель</div>
          <link-button-component href="tel:+7-4212-46-28-76">+7 (4212) 46-28-76</link-button-component>
        </div>
        <div class="v-contact">
          <div class="v-title kr-font-body-2">Бухгалтерия</div>
          <link-button-component href="tel:+7-4212-46-26-61">+7 (4212) 46-26-61</link-button-component>
        </div>
        <div class="v-contact">
          <div class="v-title kr-font-body-2">Аварийная служба</div>
          <link-button-component href="tel:+7-4212-46-24-61">+7 (4212) 46-24-61</link-button-component>
        </div>
      </div>

      <div class="v-contact-f-column">
        <div class="v-mode-work-block">
          <div class="v-mode-work">
            <div class="v-title kr-font-h4">Режим работы с собственниками</div>
            <div class="v-text kr-font-body-2">Председатель – ср, 10:00–13:00<br>Бухгалтер-расчетчик: чт, 14:00–20:00 </div>
          </div>
          <div class="v-mode-work">
            <div class="v-title kr-font-h4">Режим работы офиса</div>
            <div class="v-text kr-font-body-2">Пн-пт, 9:00–18:00<br>Перерыв: 13:00–14:00<br>Выходные: сб, вс, праздничные дни</div>
          </div>
        </div>

        <flex-button-component ref="open_request_button" @action="onOpenRequest" class="v-send-request-button">
          <template v-slot:icon>
            <icon-generate-bills-component style="width: 20px; height: 20px" />
          </template>

          <template v-slot:text>Отправить заявку</template>
        </flex-button-component>
      </div>

      <div class="v-contact-f-column v-contact-f-column-2">
        <div class="v-mode-work">
          <div class="v-title kr-font-h4">Реквизиты</div>
          <div class="v-text kr-font-body-2">
            ТСЖ «Фортуна»<br>
            680012 г. Хабаровск, ул. Флегонтова  д. 2<br>
            ИНН: 2723132676<br>
            КПП: 272301001<br>
            Р/С: 40703810970000003167<br>
            Банк: ДАЛЬНЕВОСТОЧНЫЙ БАНК СБЕРБАНКА РОССИИ ХАБАРОВСК<br>
            БИК: 040813608<br>
            Кор. счет: 30101810600000000608</div>
        </div>
      </div>

    </div>

    <div class="v-useful-phones" ref="useful_phones">
      <h3>Полезные телефоны</h3>
      <div class="v-address-block">
        <div class="v-title">
          <div class="v-main-title kr-font-h4">Травмпункт</div>
          <div class="v-sub-title kr-font-caption">взрослый</div>
        </div>
        <div class="v-address kr-font-body-2">ул. Суворова, 38</div>
        <link-button-component href="tel:+7-4212-51-01-11" class="v-num">+7 (4212) 51-01-11</link-button-component>
      </div>
      <div class="v-address-block">
        <div class="v-title">
          <div class="v-main-title kr-font-h4">Травмпункт</div>
          <div class="v-sub-title kr-font-caption">взрослый</div>
        </div>
        <div class="v-address kr-font-body-2">ул. Волочаевская, 106</div>
        <link-button-component href="tel:+7-4212-22-31-18" class="v-num">+7 (4212) 22-31-18</link-button-component>
      </div>
      <div class="v-address-block">
        <div class="v-title">
          <div class="v-main-title kr-font-h4">Травмпункт</div>
          <div class="v-sub-title kr-font-caption">детский</div>
        </div>
        <div class="v-address kr-font-body-2">ул. Прогрессивная, 6</div>
        <link-button-component href="tel:+7-4212-91-04-43" class="v-num">+7 (4212) 91-04-43</link-button-component>
      </div>
    </div>

    <request-modal-component :is-opened="requestModalIsOpened" @close="requestModalIsOpened=!requestModalIsOpened" />
  </div>
</template>

<script>
  import { Options, Vue } from "vue-class-component";
  import LinkButtonComponent from "../components/LinkButtonComponent";
  import FlexButtonComponent from "../components/FlexButtonComponent";

  import LoaderBoxComponent from "../components/LoaderBoxComponent";
  import IconGenerateBillsComponent from "../components/icons/IconGenerateBillsComponent";

  import RequestModalComponent from '../components/modals/RequestModalComponent';
  import {modalTranslateData} from "../components/ModalComponent";

  const Component = Options;
  @Component({
    components: {
      LinkButtonComponent,
      LoaderBoxComponent,
      FlexButtonComponent,
      IconGenerateBillsComponent,
      RequestModalComponent
    },
    props: {
    }
  })
  export default class Contacts extends Vue
  {
    modeQuery1024px = null;
    modeQuery1280px = null;
    lastMode = -1;

    isLoadedMap = false;

    requestModalIsOpened = false;

    created()
    {
      this.modeQuery1024px = window.matchMedia('(max-width: 1024px)');
      this.modeQuery1280px = window.matchMedia('(max-width: 1280px)');
    }

    resizeEvent()
    {
      if(this.modeQuery1024px.matches)
      {
        if(this.lastMode !== 1)
        {
          this.$refs.main_body.appendChild(this.$refs.useful_phones);
          this.$refs.main_body.appendChild(this.$refs.yandex_map);

          this.lastMode = 1;
        }
      }
      else if(this.modeQuery1280px.matches)
      {
        if(this.lastMode !== 2)
        {
          this.$refs.yandex_map_block.appendChild(this.$refs.yandex_map);
          this.$refs.yandex_map_block.appendChild(this.$refs.useful_phones);

          this.lastMode = 2;
        }
      }
      else
      {
        if(this.lastMode !== 3)
        {
          this.$refs.yandex_map_block.appendChild(this.$refs.yandex_map);
          this.$refs.main_body.appendChild(this.$refs.useful_phones);

          this.lastMode = 3;
        }
      }
    }

    async mounted()
    {
      document.title = "Контакты – ТСЖ «Фортуна» – Адрес, номер телефона, обратная связь, телефоны социальных служб";

      const _this = this;
      const scriptjs = require('scriptjs');
      scriptjs('https://api-maps.yandex.ru/2.1/?apikey=d39b6ff6-a1c2-4724-8b73-b15cb32cd2dc&lang=ru_RU', function () {
        ymaps.ready(() => {
          _this.isLoadedMap = true;
          const map = new ymaps.Map(_this.$refs.yandex_map, {
            center: [48.433641, 135.107266],
            controls: ['zoomControl'],
            zoom: 16
          });

          map.geoObjects.add(new ymaps.Placemark(map.getCenter(), {hideIcon: false}));

          map.behaviors.disable('scrollZoom');
          map.behaviors.disable('drag');
        });
      });

      window.addEventListener("resize", this.resizeEvent, false);
      window.addEventListener("orientationchange", this.resizeEvent, false);
      this.resizeEvent();
    }

    beforeUnmount()
    {
      window.removeEventListener("resize", this.resizeEvent);
      window.removeEventListener("orientationchange", this.resizeEvent);
    }

    onOpenRequest()
    {
      //modalTranslateData.el = this.$refs.open_request_button.$el;
      this.requestModalIsOpened = true;
    }
  }
</script>
