<style scoped lang="scss">

    .v-news
    {
        text-align: left;
    }

    .v-preview-block
    {
        width: 100%;
        text-align: left;
    }

    .v-single-block
    {
        display: inline-block;

        $marginRight: 16;

        width: 308px;

        &:not(:last-child)
        {
            margin-right: #{$marginRight}px;
        }

        text-align: left;

        vertical-align: text-top;
    }

    .v-block-title
    {
        width: 100%;
        display: block;
        margin-bottom: 16px;
        text-align: left;
    }

    @media (max-width: 1300px)
    {
        $marginBottomNewsBlockPx: 24px;

        .v-block-title
        {
            width: 944px;
            margin-left: auto;
            margin-right: auto;
        }

        .v-preview-block
        {
            display: inline-block;

            width: 944px;
        }

        .v-single-block
        {
            width: 464px;

            &:not(:last-child)
            {
                margin-right: 0;
            }

            &:nth-child(1),&:nth-child(2)
            {
                margin-bottom: $marginBottomNewsBlockPx;
            }

            &:nth-child(1), &:nth-child(3)
            {
                margin-right: 16px;
            }
        }
    }

    @media (max-width: 990px)
    {
        .v-block-title
        {
            width: 560px;
            margin-left: auto;
            margin-right: auto;
        }

        .v-preview-block
        {
            width: 560px;
        }

        .v-single-block
        {
            width: 276px;

            &:nth-child(1),&:nth-child(2)
            {
                margin-bottom: 16px;
            }

            &:nth-child(1), &:nth-child(3)
            {
                margin-right: 8px;
            }
        }
    }

    @media (max-width: 600px)
    {
        .v-block-title
        {
            width: fit-content;
            margin-left: 20px;
            margin-right: unset;
        }

        .v-preview-block
        {
            width: 100%;
        }

        .v-single-block
        {
            width: calc(100vw - 60px);

            margin: 0;

            &:nth-child(1), &:nth-child(3)
            {
                margin-right: 0;
            }

            &:nth-child(1),&:nth-child(2)
            {
                margin-bottom: 0;
            }
        }
    }
</style>

<style lang="scss">
    .v-preview-block
    {
        .splide__arrows,.splide__pagination
        {
            visibility: hidden;
        }
    }
</style>

<template>
    <div>
        <div class="v-block-title">
            <title-with-link-component :to="to">
                <slot name="link"></slot>
            </title-with-link-component>
        </div>
        <div class="v-preview-block">
            <template v-if="items">
                <template v-if="useSlider">
                    <splide :options="splideOptions">
                        <template v-for="item in items">
                            <splide-slide>
                                <div class="v-single-block">
                                    <slot name="item" :item="item"></slot>
                                </div>
                            </splide-slide>
                        </template>
                    </splide>
                </template>
                <template v-else>
                    <template v-for="item in items">
                        <div class="v-single-block">
                            <slot name="item" :item="item"></slot>
                        </div>
                    </template>
                </template>
            </template>
            <template v-else>
                <template v-if="useSlider">
                    <splide :options="splideOptions">
                        <template v-for="numBlock in 4">
                            <splide-slide>
                                <div class="v-single-block">
                                    <slot name="loading"></slot>
                                </div>
                            </splide-slide>
                        </template>
                    </splide>
                </template>
                <template v-else>
                    <template v-for="numBlock in 4">
                        <div class="v-single-block">
                            <slot name="loading"></slot>
                        </div>
                    </template>
                </template>
            </template>
        </div>
    </div>
</template>

<script>
    import { Options, Vue } from "vue-class-component";

    import LoaderBoxComponent from './LoaderBoxComponent';

    import TitleWithLinkComponent from './TitleWithLinkComponent';

    import { Splide, SplideSlide } from '@splidejs/vue-splide';
    import '@splidejs/splide/dist/css/themes/splide-default.min.css';



    const Component = Options;
    @Component({
        components: {
            LoaderBoxComponent,
            Splide,
            SplideSlide,
            TitleWithLinkComponent
        },
        props: {
            to: String,
            items: Array
        }
    })
    export default class PreviewBlockComponent extends Vue {
        useSlider = false;

        modeQueryMax600px = null;

        splideOptions = {
            rewind : true,
            padding: {
                right: '20px',
                left : '20px',
            },
            autoWidth: true,
            focus    : 'center',
            gap    : '20px',
        };

        mounted()
        {
            this.modeQueryMax600px = window.matchMedia('(max-width: 600px)');

            window.addEventListener("resize", this.resizeViewport, false);
            window.addEventListener("orientationchange", this.resizeViewport, false);
            this.resizeViewport();
        }

        beforeUnmount()
        {
            window.removeEventListener("resize", this.resizeViewport, false);
            window.removeEventListener("orientationchange", this.resizeViewport, false);
        }

        resizeViewport()
        {
            if(this.modeQueryMax600px.matches)
            {
                this.useSlider = true;
            }
            else
            {
                this.useSlider = false;
            }
        }
    }
</script>