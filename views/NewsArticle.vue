<style scoped lang="scss">
  @import "../stylesheets/kira-fonts";

  .kr-body
  {
    h1
    {
      max-width: 678px;

      color: var(--kr-color-layout-black-metallic);
      margin: 0 auto 8px;

      text-align: left;

      @include kiraFont(h3);
    }
  }

  .v-date
  {
    max-width: 678px;
    margin-left: auto;
    margin-right: auto;
    color: var(--kr-color-main-help-text);

    margin-bottom: 24px;

    text-align: left;

    @include kiraFont(body-2);
  }

  .v-img
  {
    display: flex;

    margin-bottom: 32px;
    width: 760px;
    height: 429px;

    margin-left: auto;
    margin-right: auto;

    border-radius: 8px;

    overflow: hidden;
  }

  .v-text
  {
    max-width: 678px;

    color: var(--kr-color-main-plain-text);
    text-align: left;

    margin-left: auto;
    margin-right: auto;

    @include kiraFont(body-2);

    p
    {
      margin-top: 16px;
      margin-bottom: 16px;
    }
  }

  @media (max-width: 945px)
  {
    .kr-body
    {
      h1
      {
        max-width: 560px;
      }
    }

    .v-date
    {
      max-width: 560px;
    }

    .v-img
    {
      width: 560px;
      height: 317px;
    }

    .v-text
    {
      max-width: 560px;
    }

  }

  @media (max-width: 640px)
  {
    .kr-body
    {
      h1
      {
        max-width: 400px;
      }
    }

    .v-date
    {
      max-width: 400px;

      @include kiraFont(caption);
    }

    .v-img
    {
      width: 440px;
      height: 249px;
    }

    .v-text
    {
      max-width: 400px;
    }
  }

  @media (max-width: 475px)
  {
    .kr-body
    {
      h1
      {
        max-width: 280px;

        margin-bottom: 12px;

        @include kiraFont(h4);
      }
    }

    .v-date
    {
      max-width: 280px;
    }

    .v-img
    {
      width: 320px;
      height: 181px;
    }

    .v-text
    {
      max-width: 280px;
    }
  }
</style>

<template>
  <div class="kr-body kr-body-margin-top kr-body-margin-bottom">
    <div v-if="article" class="v-article">
      <h1>{{article.title}}</h1>
      <div class="v-date">{{getStringHumanDate(article.date)}}</div>
      <template v-if="article.content">
        <template v-for="block in article.content.blocks">
          <attachment-image-component
                  v-if="block.type === 'attachment_image'"
                  class="v-img"
                  :attachment="article.attachments.find((attachment) => attachment.id === block.data.attachment_id)" />
          <p
                  class="v-text"
                  v-else-if="block.type === 'paragraph'"
                  v-html="block.data.text"></p>
        </template>
      </template>
    </div>
  </div>
</template>

<script>
  import {Options, Vue} from "vue-class-component";
  import TradeArticlesManager from "../lib/trade/TradeArticlesManager";
  import AttachmentImageComponent from "../components/AttachmentImageComponent";
  import DateManager from "../lib/DateManager";

  const Component = Options;
  @Component({
    components: {
      AttachmentImageComponent
    },
    props: {
      id: [Number, String]
    }
  })
  export default class NewArticle extends Vue
  {
    article = null;

    async beforeMount()
    {
      this.article = await TradeArticlesManager.getArticleById(this.id);
      document.title = `${this.article.title} – ТСЖ «Фортуна»`;
    }

    getStringHumanDate(dateStr)
    {
      return DateManager.getStringHumanDateTimeFromString(dateStr);
    }
  }
</script>
