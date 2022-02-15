<style scoped lang="scss">

    .v-single-block
    {
        text-decoration: none;
        height: 253px;
    }

    .v-img
    {
        display: block;

        width: 100%;
        height: 173px;
        border-radius: 8px;
        overflow: hidden;
    }

    .v-title
    {
        display: block;

        margin-top: 16px;
        width: 100%;
        max-height: 40px;

        color: var(--kr-color-main-plain-text);

        overflow: hidden;

        &.v-loading
        {
            height: 40px;
            width: calc(80%);
        }
    }

    .v-date
    {
        display: block;

        margin-top: 8px;
        width: 100%;
        height: 16px;

        &.v-loading
        {
            width: 80px;
            border-radius: 4px;
        }

        color: var(--kr-color-main-help-text);
    }

    @media (max-width: 1300px)
    {
        .v-single-block
        {
            height: 340px;
        }

        .v-img
        {
            height: 260px;
        }
    }

    @media (max-width: 990px)
    {
        .v-single-block
        {
            height: 253px;
        }

        .v-img
        {
            height: 173px;
        }
    }

    @media (max-width: 600px)
    {
        .v-single-block
        {
            height: calc(289px - 213px + ((100vw - 60px) * (213 / 380)));
        }

        .v-img
        {
            height: calc((100vw - 60px) * (213 / 380));
        }

        .v-title
        {
            margin-top: 12px;
        }
    }
</style>

<template>
    <div>
        <preview-block-component :items="articles" to="/news">
            <template v-slot:link>Новости</template>
            <template v-slot:item="slotProps">
                <router-link class="v-single-block" :to="'/news/' + slotProps.item.id + '_' + cyrillicToTranslit().transform(slotProps.item.title, '_').toLowerCase()"
                >
                    <div class="v-img">
                        <attachment-image-component
                                v-if="slotProps.item.attachments[0]"
                                :attachment="slotProps.item.attachments[0]"/>
                        <no-image-component v-else/>
                    </div>
                    <div class="v-title kr-font-h4">{{slotProps.item.title}}</div>
                    <div class="v-date kr-font-caption">{{getStringHumanDate(slotProps.item.date)}}</div>
                </router-link>
            </template>
            <template v-slot:loading>
                <div class="v-single-block">
                    <loader-box-component class="v-img"/>
                    <loader-box-component class="v-title v-loading"/>
                    <loader-box-component class="v-date v-loading"/>
                </div>
            </template>
        </preview-block-component>
    </div>
</template>

<script>
    import { Options, Vue } from "vue-class-component";
    import TradeArticlesManager from "../lib/trade/TradeArticlesManager";

    import LoaderBoxComponent from './LoaderBoxComponent';

    import DateManager from "../lib/DateManager";

    import AttachmentImageComponent from "./AttachmentImageComponent";
    import NoImageComponent from "./NoImageComponent";

    import cyrillicToTranslit from "cyrillic-to-translit-js";

    import PreviewBlockComponent from "./PreviewBlockComponent";

    const Component = Options;
    @Component({
        components: {
            LoaderBoxComponent,
            AttachmentImageComponent,
            PreviewBlockComponent,
            NoImageComponent
        },
        props: {
        }
    })
    export default class NewsPreviewBlockComponent extends Vue {
        articles = null;
        cyrillicToTranslit = cyrillicToTranslit;

        async created()
        {
            const articlesData = await TradeArticlesManager.getArticles({ limit: 4, category_id: 1 });
            this.articles = articlesData.items;
        }

        getStringHumanDate(dateStr)
        {
            return DateManager.getStringHumanDateTimeFromString(dateStr);
        }
    }
</script>