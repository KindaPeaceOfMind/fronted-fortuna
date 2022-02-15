<style scoped lang="scss">
    @import "../stylesheets/kira-fonts";

    .v-block-title
    {
        color: var(--kr-color-main-header);
        text-align: left;

        width: fit-content;
        display: inline-block;
    }

    .v-icon-arrow
    {
        width: 20px;
        height: 20px;

        transition: margin-left .3s cubic-bezier(0.23, 0.74, 0.53, 1.06);
    }

    .v-text
    {
        display: inline-block;
    }

    .v-arrow-box
    {
        margin-left: 4px;
        display: inline-block;
        width: 20px + 8px;
    }

    .v-title-with-link
    {
        &:hover
        {
            .v-block-title
            {
                color: var(--kr-color-feedback-active-2);

                .v-icon-arrow
                {
                    margin-left: 8px;
                }
            }
        }

        &:active
        {
            .v-block-title
            {
                color: var(--kr-color-feedback-active-3);
            }
        }

    }
</style>

<template>
    <router-link class="v-title-with-link" :to="to">
        <div class="v-block-title kr-font-h3" >
            <div class="v-text">
                <slot></slot>
            </div>
            <div class="v-arrow-box">
                <icon-arrow-component class="v-icon-arrow" />
            </div>
        </div>
    </router-link>
</template>

<script>
    import { Options, Vue } from "vue-class-component";
    import IconArrowComponent from './icons/IconArrowComponent';

    const Component = Options;
    @Component({
        components: {
            IconArrowComponent
        },
        props: {
            to: String
        }
    })
    export default class TitleWithLinkComponent extends Vue
    {

    }
</script>