<style scoped lang="scss">
    @import '../stylesheets/kira-fonts';

    .v-main-title
    {
        text-align: left;

        @include kiraFont(h1);

        margin-bottom: 32px;
    }

    .v-articles
    {
        text-align: left;
    }

    .v-link-box
    {
        text-decoration: none;
    }

    .v-single-block
    {
        width: 308px;

        vertical-align: text-top;

        display: inline-block;

        margin-right: 16px;

        &:nth-child(4n) {
            margin-right: 0;
        }
    }

    .v-date
    {
        width: 100%;

        color: var(--kr-color-main-help-text);
    }

    .v-icon-loader
    {
        margin-left: auto;
        margin-right: auto;
        color: var(--kr-color-main-help-text);

        margin-top: 8px;
    }

    @media (max-width: 1310px)
    {
        .vc-card-articles
        {
            width: 944px;
        }

        .v-main-title
        {
            margin-bottom: 40px;
        }

        .v-single-block
        {
            width: 464px;

            margin-right: 16px;

            &:nth-child(2n) {
                margin-right: 0;
            }
        }
    }

    @media (max-width: 1024px)
    {
        .vc-card-articles
        {
            width: 276px * 2 + 8px;
        }

        .v-main-title
        {
            margin-bottom: 24px;
        }

        .v-single-block
        {
            margin-right: 8px;

            width: 276px;

            &:nth-child(2n) {
                margin-right: 0;
            }
        }
    }

    @media (max-width: 640px)
    {
        .vc-card-articles
        {
            width: 380px;
        }

        .v-main-title
        {
            @include kiraFont(h3);
            margin-bottom: 16px;
        }

        .v-single-block
        {
            margin-right: 0;

            width: 380px;
        }
    }

    @media (max-width: 440px)
    {
        .vc-card-articles
        {
            width: 260px;
        }

        .v-single-block
        {
            width: 260px;
        }
    }
</style>

<template>
    <div class="vc-card-articles">
        <div class="v-main-title">
            <slot name="title"></slot>
        </div>
        <div class="v-articles" ref="articles_block">
            <div
                    class="v-single-block"
                    v-for="article in articles"
                    :key="article.id"
            >
                <slot name="article" :article="article"></slot>
            </div>
        </div>
        <div v-if="isLoadingData">
            <icon-spinner-component class="v-icon-loader" />
        </div>
    </div>
</template>

<script>
    import { Options, Vue } from "vue-class-component";
    import TradeArticlesManager from "../lib/trade/TradeArticlesManager";
    import IconSpinnerComponent from "./icons/IconSpinnerComponent";

    const Component = Options;
    @Component({
        components: {
            IconSpinnerComponent
        },
        props: {
            optionsBase: Object
        }
    })
    export default class CardArticlesComponent extends Vue
    {
        countPages = 0;
        currentPage = 0;

        isLoadingData = false;

        articles = [];

        async beforeMount()
        {
            const options = Object.assign({}, this.optionsBase);
            const articlesData = await TradeArticlesManager.getArticles(options);

            this.countPages = Math.ceil(articlesData.meta.count / articlesData.meta.limit);
            this.currentPage = articlesData.meta.page;
            for(let article of articlesData.items)
            {
                this.articles.push(article);
            }

            await this.$nextTick(() => {
                if (this.currentPage < this.countPages) {
                    window.addEventListener('scroll', this.checkUpdatesBasedOnScreenPosition);
                    window.addEventListener("resize", this.checkUpdatesBasedOnScreenPosition);
                    window.addEventListener("orientationchange", this.checkUpdatesBasedOnScreenPosition);
                    this.checkUpdatesBasedOnScreenPosition();
                }
            });
        }

        beforeUnmount()
        {
            window.removeEventListener('scroll', this.checkUpdatesBasedOnScreenPosition);
            window.removeEventListener("resize", this.checkUpdatesBasedOnScreenPosition);
            window.removeEventListener("orientationchange", this.checkUpdatesBasedOnScreenPosition);
        }

        async checkUpdatesBasedOnScreenPosition()
        {
            if(this.isLoadingData)
            {
                return;
            }

            const articlesRect = this.$refs.articles_block.getBoundingClientRect();
            if(articlesRect.top + this.$refs.articles_block.offsetHeight < window.innerHeight)
            {
                this.currentPage++;

                const options = Object.assign({}, this.optionsBase);
                options.page = this.currentPage;

                this.isLoadingData = true;

                const articlesData = await TradeArticlesManager.getArticles(options);
                for(let article of articlesData.items)
                {
                    this.articles.push(article);
                }

                this.isLoadingData = false;

                if(this.currentPage >= this.countPages)
                {
                    window.removeEventListener('scroll', this.checkUpdatesBasedOnScreenPosition);
                    window.removeEventListener("resize", this.checkUpdatesBasedOnScreenPosition);
                    window.removeEventListener("orientationchange", this.checkUpdatesBasedOnScreenPosition);
                }
                else
                {
                    await this.$nextTick(() => {
                        this.checkUpdatesBasedOnScreenPosition();
                    });
                }
            }
        }
    }
</script>
