<style scoped lang="scss">
    @import "../stylesheets/kira-fonts";

    .v-footer
    {
        position: relative;
        width: 100%;
        height: 120px;

        border-top: 1px solid #D4D4D9;
    }

    .v-logo-btn
    {
        position: absolute;
        width: 81px;
        height: 56px;

        left: 32px;
        top: 50%;

        transform: translateY(-50%);
    }

    .v-icon-logo
    {
        position: absolute;
        width: 100%;
        height: 100%;
    }

    .v-text
    {
        position: absolute;
        left: 137px;
        top: 50%;
        transform: translateY(-50%);

        color: var(--kr-color-main-help-text);
    }

    .v-logo
    {
        position: absolute;
        right: 32px;
        top: 50%;

        transform: translateY(-50%);
    }

    @media (max-width: 440px)
    {
        .v-footer
        {
            height: 100px;
        }

        .v-logo
        {
            top: 12px;
            right: 20px;

            transform: unset;
        }

        .v-logo-btn
        {
            top: 12px;
            left: 20px;

            transform: unset;

            width: 69px;
            height: 48px;
        }

        .v-text
        {
            top: unset;

            left: 50%;
            bottom: 16px;

            transform: translateX(-50%);
        }
    }
</style>

<template>
    <div class="v-footer">
        <router-link @click.capture="isOpenedMenu=false" class="v-logo-btn" tabindex="0" to="/">
            <icon-logo-component class="v-icon-logo" />
        </router-link>

        <div class="v-text kr-font-caption">© {{year}} ТСЖ «Фортуна»</div>
        <kira-logo-component class="v-logo"/>
    </div>
</template>

<script>
    import { Options, Vue } from "vue-class-component";

    import IconComponent from './IconComponent';
    import IconLogoComponent from "./icons/IconLogoComponent";

    import KiraLogoComponent from "./KiraLogoComponent";

    const Component = Options;
    @Component({
        components: {
            IconLogoComponent,
            IconComponent,
            KiraLogoComponent
        },
        props: {

        }
    })
    export default class FooterComponent extends Vue
    {
        year = new Date().getFullYear();
    }
</script>