<style scoped lang="scss">
  @import '../stylesheets/kira-fonts';

  .v-card-articles
  {
    margin-right: auto;
    margin-left: auto;
  }

  .v-single-block
  {
    display: block;
    height: 253px;
    margin-bottom: 32px;
    text-decoration: none;
  }

  .v-img
  {
    width: 308px;
    height: 173px;

    margin-bottom: 16px;

    overflow: hidden;
    border-radius: 8px;
  }

  .v-title
  {
    width: 308px;
    max-height: 40px;

    margin-bottom: 8px;
    overflow: hidden;

    color: var(--kr-color-main-plain-text);
  }

  .v-date
  {
    width: 100%;

    color: var(--kr-color-main-help-text);
  }

  @media (max-width: 1310px)
  {
    .v-single-block
    {
      height: 340px;
      margin-bottom: 24px;
    }

    .v-img
    {
      width: 464px;
      height: 260px;
    }

    .v-title
    {
      width: 464px;
    }

  }

  @media (max-width: 1024px)
  {
    .v-img
    {
      width: 276px;
      height: 173px;
    }

    .v-single-block
    {
      margin-bottom: 16px;
      height: 253px;
    }

    .v-title
    {
      width: 276px;
    }
  }

  @media (max-width: 640px)
  {
    .v-single-block
    {
      height: 289px;
    }

    .v-img
    {
      width: 380px;
      height: 213px;

      margin-bottom: 12px;
    }

    .v-title
    {
      width: 380px;
      margin-bottom: 8px;
    }
  }

  @media (max-width: 440px)
  {
    .v-single-block
    {
      height: 222px;
    }

    .v-img
    {
      width: 260px;
      height: 146px;
    }

    .v-title
    {
      width: 260px;
    }
  }
</style>

<template>
  <div class="kr-body kr-body-margin-top kr-body-margin-bottom">
    <card-articles-component class="v-card-articles" :options-base="{ limit: 8, category_id: 1 }">
      <template v-slot:title>Новости</template>
      <template v-slot:article="slotProps">
        <router-link class="v-single-block"
                     :to="'/news/' + slotProps.article.id + '_' + cyrillicToTranslit().transform(slotProps.article.title, '_').toLowerCase()"
        >
          <div class="v-img">
            <attachment-image-component
                    v-if="slotProps.article.attachments[0]"
                    :attachment="slotProps.article.attachments[0]"/>
            <no-image-component v-else />
          </div>
          <div class="v-title kr-font-h4">{{slotProps.article.title}}</div>
          <div class="v-date kr-font-caption">{{getStringHumanDate(slotProps.article.date)}}</div>
        </router-link>
      </template>
    </card-articles-component>
  </div>
</template>

<script>
  import { Options, Vue } from "vue-class-component";

  import AttachmentImageComponent from "../components/AttachmentImageComponent";

  import DateManager from "../lib/DateManager";
  import cyrillicToTranslit from "cyrillic-to-translit-js";
  import NoImageComponent from "../components/NoImageComponent";

  import CardArticlesComponent from "../components/CardArticlesComponent";

  const Component = Options;
  @Component({
    components: {
      NoImageComponent,
      AttachmentImageComponent,
      CardArticlesComponent
    },
    props: {
    }
  })
  export default class News extends Vue
  {
    cyrillicToTranslit = cyrillicToTranslit;

    mounted()
    {
      document.title = "Новости – ТСЖ «Фортуна» – Актуальная информация, важные новости и объявления для жильцов";
    }

    getStringHumanDate(dateStr)
    {
      return DateManager.getStringHumanDateTimeFromString(dateStr);
    }
  }
</script>
