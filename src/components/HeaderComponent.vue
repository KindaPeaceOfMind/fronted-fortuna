<style scoped lang="scss">
    @import "../stylesheets/kira-fonts";

    $minMarginMenuItem: 8;
    $maxMarginMenuItem: 20;

    $maxWidthHeader: 1320;
    $mediumWidthHeader: 980;

    $maxWidthMenu: 777;
    $mediumWidthMenu: 437;

    $widthNumberBox: 167;

    .v-header
    {
        position: relative;
        height: 96px;

        background: white;

        transition: height .56s cubic-bezier(0.52, 0.16, 0.24, 1), box-shadow .44s .2s cubic-bezier(0.52, 0.16, 0.24, 1);

        overflow: hidden;
    }

    .v-header-main
    {
        position: relative;
        width: 100%;
        height: 96px;
        top: 0;

        transition: height 300ms ease-in-out;
    }

    .v-icon-header
    {
        width: 40px;
        height: 40px;
    }

    .v-logo
    {
        display: inline-block;
        width: 92px;
        height: 64px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .v-logo-btn
    {
        display: inline-block;
        position: absolute;
        width: 92px;
        height: 100%;
        left: 0;

        border-radius: 8px;
    }

    .v-number-box
    {
        position: absolute;
        width: #{$widthNumberBox}px;
        height: 100%;

        right: 265px;
    }

    .v-main-number
    {
        text-decoration: none;

        color: var(--kr-color-main-plain-text);
    }

    .v-number-wrapper
    {
        position: absolute;
        display: inline-block;
        width: 100%;
        height: 60px;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);

        div
        {
            position: absolute;
            left: 0;
        }
    }

    .v-sub-number
    {
        color: var(--kr-color-main-help-text);

        &.v-num1
        {
            top: 24px;
        }

        &.v-num2
        {
            top: 44px;
        }
    }

    .v-menu-box
    {
        position: absolute;
        height: 100%;
        left: 96px;
        right: 265px + $widthNumberBox;
    }

    .v-menu
    {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);

        width: 100%;
        height: 64px;
    }

    .v-menu-item
    {
        &:not(:last-child)
        {
            //margin-right: calc(#{$maxMarginMenuItem}px - ((#{$maxWidthMenu}px - 100%) /
            //                #{($maxWidthMenu - $mediumWidthMenu)}) * #{$maxMarginMenuItem - $minMarginMenuItem} );
            margin-right: 16px;
        }
    }

    .v-send-request-button
    {
        position: absolute;
        right: 0;
        top: 50%;
        transform: translateY(-50%);
    }

    .v-burger-menu
    {
        position: absolute;
        width: 52px;
        height: 100%;
        display: none;
        left: 0;
        top: 0;

        cursor: pointer;

        user-select: none;

        -webkit-tap-highlight-color: transparent;
    }

    .v-icon-burger
    {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);

        width: 16px;
        height: 14px;

        color: #2D2D2D;
    }

    .v-menu-divider-1,.v-menu-divider-2
    {
        display: none;
        position: absolute;
        left: 50%;

        background-color: #E1E1E8;
    }

    .v-menu-divider-1
    {
        width: 256px;
        height: 1px;

        transform: translateX(-50%) rotate(90deg) ;

        top: 64px + 136px;
    }

    .v-menu-divider-2
    {
        width: 256px;
        height: 1px;

        transform: translateX(-50%);

        top: 64px + 136px;
    }

    .v-header-back
    {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;

        transition: background-color 300ms ease-in-out;

        pointer-events: none;
    }

    .v-header-back-show
    {
        pointer-events: auto;

        background: rgba(0, 0, 0, 0.2);
    }

    .v-icon-meter
    {
        width: 20px;
        height: 20px;
        color: var(--kr-color-main-white);
    }

    @media (max-width: 1280px)
    {
        .v-menu-item
        {
            &:not(:last-child)
            {
                margin-right: 0;
            }
        }

        .v-number-box
        {
            right: 257px;
        }
    }

    @media (max-width: 965px)
    {
        $headerHeightPx: 80px;

        .v-header
        {
            height: $headerHeightPx;

            &.v-header-opened
            {
                height: 210px;

                box-shadow: 0 2px 6px rgba(0,0,0,.08), 0 4px 32px rgba(0,0,0,.16);

                .v-menu
                {
                    transform: translate(-50%, -50%);
                    opacity: 1;

                    pointer-events: unset;
                }
            }
        }

        .v-menu-box
        {
            top: 96px;
            left: 0;

            width: 100%;
            height: 98px;
        }

        .v-menu-item
        {
            margin: 0;

            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);

            width: 100%;
            height: 100%;
        }

        .v-menu
        {
            grid-template-columns: repeat(auto-fit, minmax(0px, 1fr));
            display: inline-grid;

            transition: transform .56s cubic-bezier(0.52, 0.16, 0.24, 1), opacity .4s cubic-bezier(0.52, 0.16, 0.24, 1);

            transform: scaleY(0.8) translate(-50%, -100%);
            opacity: 0;

            pointer-events: none;
        }

        .v-header-main
        {
            height: $headerHeightPx;
        }

        .v-burger-menu
        {
            display: inline-block;
        }

        .v-logo-btn
        {
            width: 80px;
            left: 52px;
        }

        .v-logo
        {
            width: 80px;
            height: 56px;
        }

        .v-send-request-button
        {
            right: 16px;
        }

        .v-number-box
        {
            right: 88px;
        }

    }

    @media (max-width: 440px)
    {
        .v-header
        {
            height: 64px;

            &.v-header-opened
            {
                height: 466px;

                .v-menu-divider-1,.v-menu-divider-2
                {
                    width: 256px;
                    opacity: 1;
                }

                .v-menu-divider-1
                {
                    transition-delay: 0.2s;
                }

                .v-menu-divider-2
                {
                    transition-delay: 0.3s;
                }

                .v-menu
                {
                    transform: translateX(-50%);

                    pointer-events: unset;
                }

                .v-menu-item
                {
                    transform: translate(-50%, -50%);
                    opacity: 1;
                }

                .v-menu-item:nth-child(1),.v-menu-item:nth-child(2)
                {
                    transition-delay: 0.0s;
                }

                .v-menu-item:nth-child(3),.v-menu-item:nth-child(4)
                {
                    transition-delay: 0.1s;
                }

                .v-number-box
                {
                    transform: unset;
                    opacity: 1;
                    pointer-events: unset;
                    transition-delay: 0.2s;
                }
            }
        }

        .v-header-main
        {
            height: 64px;
        }

        .v-menu
        {
            grid-template-columns: repeat(2, minmax(0, 1fr));
            grid-template-rows: repeat(2, minmax(128px, 1fr));

            transform: unset;
            opacity: 1;
        }

        .v-menu-item
        {
            transform: scaleY(0.8) translate(-50%, -100%);
            opacity: 0;
        }

        .v-menu-item:nth-child(1),.v-menu-item:nth-child(2)
        {
            transition: transform .56s cubic-bezier(0.52, 0.16, 0.24, 1), opacity .4s cubic-bezier(0.52, 0.16, 0.24, 1);
            transition-delay: 0.2s;
        }

        .v-menu-item:nth-child(3),.v-menu-item:nth-child(4)
        {
            transition: transform .46s cubic-bezier(0.52, 0.16, 0.24, 1), opacity .3s cubic-bezier(0.52, 0.16, 0.24, 1);
            transition-delay: 0.1s;
        }

        .v-logo
        {
            width: 69px;
            height: 48px;
        }

        .v-logo-btn
        {
            width: 69px;
            height: 100%;
            left: 60px;
        }

        .v-menu-box
        {
            top: 64px + 8px;
        }

        .v-menu
        {
            top: 0;
            transform: translateX(-50%);
        }

        .v-number-box
        {
            display: inline-block;
            width: 100%;
            height: 100%;
            left: 32px;
            top: 64px + 312px;
            text-align: left;

            transform: scaleY(0.8) translateY(-50%);
            opacity: 0;

            transition: transform .36s cubic-bezier(0.52, 0.16, 0.24, 1), opacity .2s cubic-bezier(0.52, 0.16, 0.24, 1);
            transition-delay: 0.1s;

            pointer-events: none;
        }

        .v-number-wrapper
        {
            top: 0;
            transform: unset;
            left: 0;
        }

        .v-send-request-button
        {
            right: 8px;
        }

        .v-burger-menu
        {
            width: 52px;
        }

        .v-menu-divider-1,.v-menu-divider-2
        {
            display: inline-block;
        }

        .v-menu-divider-1
        {
            width: 0px;
            opacity: 0;

            transition: width .46s cubic-bezier(0.52, 0.16, 0.24, 1), opacity .3s cubic-bezier(0.52, 0.16, 0.24, 1);
            transition-delay: 0.1s;
        }

        .v-menu-divider-2
        {
            width: 0px;
            opacity: 0;

            transition: width .36s cubic-bezier(0.52, 0.16, 0.24, 1), opacity .2s cubic-bezier(0.52, 0.16, 0.24, 1);
            transition-delay: 0.0s;
        }
    }
</style>

<template>
    <div class="v-header" :class="{ 'v-header-opened': isOpenedMenu }">
        <teleport to="#v-header-back" v-if="isMounted">
            <div class="v-header-back" :class="{ 'v-header-back-show': isOpenedMenu }" @click="isOpenedMenu=false"></div>
        </teleport>

        <div class="v-header-main">
            <div class="v-burger-menu" @click="isOpenedMenu=!isOpenedMenu" tabindex="0">
                <hamburgers-component :active="isOpenedMenu" class="v-icon-burger" />
            </div>

            <router-link @click.capture="isOpenedMenu=false" class="v-logo-btn" tabindex="0" to="/">
                <icon-logo-component class="v-logo" />
            </router-link>

            <div class="v-menu-box">
                <div class="v-menu kr-font-navigation">
                    <header-menu-item-component @click.capture="isOpenedMenu=false" class="v-menu-item" to="/news">
                        <template v-slot:header>
                            <icon-news-component class="v-icon-header"/>
                        </template>
                        <template v-slot:body><div class="v-text-menu-item">Новости</div></template>
                    </header-menu-item-component>

                    <header-menu-item-component @click.capture="isOpenedMenu=false" class="v-menu-item" to="/arts">
                        <template v-slot:header>
                            <icon-art-component class="v-icon-header"/>
                        </template>
                        <template v-slot:body><div class="v-text-menu-item">Галерея</div></template>
                    </header-menu-item-component>

                    <header-menu-item-component @click.capture="isOpenedMenu=false" class="v-menu-item" to="/documents">
                        <template v-slot:header>
                            <icon-documents-component class="v-icon-header"/>
                        </template>
                        <template v-slot:body><div class="v-text-menu-item">Документы</div></template>
                    </header-menu-item-component>

                    <header-menu-item-component @click.capture="isOpenedMenu=false" class="v-menu-item" to="/contacts">
                        <template v-slot:header>
                            <icon-contacts-component class="v-icon-header"/>
                        </template>
                        <template v-slot:body><div class="v-text-menu-item">Контакты</div></template>
                    </header-menu-item-component>
                </div>
            </div>

            <div class="v-menu-divider-1"></div>
            <div class="v-menu-divider-2"></div>

            <div class="v-number-box">
                <div class="v-number-wrapper">
                    <a href="tel:+7-4212-46-24-61" class="v-main-number kr-font-h4">+7 (4212) 46-24-61</a>
                    <div class="v-sub-number v-num1 kr-font-caption">Заявки: пн-пт, 9:00–18:00</div>
                    <div class="v-sub-number v-num2 kr-font-caption">Аварийная служба 24/7</div>
                </div>
            </div>

            <flex-button-component @action="onOpenMetersModalData"
                                   class="v-send-request-button"
                                   :mode="isMiniSendRequestButton ? 'icon-only' : 'full'" ref="open_meters_button">
                <template v-slot:icon>
                    <icon-meter-component class="v-icon-meter" />
                </template>

                <template v-slot:text>Показания счетчиков</template>
            </flex-button-component>
        </div>

        <meters-data-modal-component :is-opened="metersDataModalIsOpened" @close="metersDataModalIsOpened=false" />
    </div>
</template>

<script>
    import { Options, Vue } from "vue-class-component";

    import IconArtComponent from "./icons/IconArtComponent";
    import IconContactsComponent from "./icons/IconContactsComponent";
    import IconDocumentsComponent from "./icons/IconDocumentsComponent";
    import IconNewsComponent from "./icons/IconNewsComponent";

    import IconMeterComponent from "./icons/IconMeterComponent";

    import IconLogoComponent from "./icons/IconLogoComponent";

    import FlexButtonComponent from "./FlexButtonComponent";

    import HeaderMenuItemComponent from "./HeaderMenuItemComponent";

    import HamburgersComponent from "./base/HamburgersComponent";

    import MetersDataModalComponent from './modals/MetersDataModalComponent';
    import {modalTranslateData} from "@/components/ModalComponent";


    const Component = Options;
    @Component({
        components: {
            HeaderMenuItemComponent,
            IconArtComponent,
            IconContactsComponent,
            IconDocumentsComponent,
            IconNewsComponent,

            IconMeterComponent,

            FlexButtonComponent,

            IconLogoComponent,

            MetersDataModalComponent,
            HamburgersComponent
        },
        props: {
        },
        watch: {
            isOpenedMenu: function(newVal) {
                if(newVal)
                {
                    this.$emit('opened-menu');
                }
                else
                {
                    this.$emit('closed-menu');
                }
            }
        },
        emits: ['opened-menu', 'closed-menu']
    })
    export default class HeaderComponent extends Vue {
        mediumModeQuery = null;

        isMiniSendRequestButton = false;

        isOpenedMenu = false;

        isMounted = false;

        metersDataModalIsOpened = false;

        resizeEvent()
        {
            const matchesMediumModeQuery = this.mediumModeQuery.matches;

            this.isMiniSendRequestButton = !!matchesMediumModeQuery;

            if(!matchesMediumModeQuery)
            {
                this.isOpenedMenu = false;
            }
        }

        created()
        {
            this.mediumModeQuery = window.matchMedia('(max-width: 965px)');
        }

        mounted()
        {
            this.isMounted = true;

            window.addEventListener("resize", this.resizeEvent, false);
            window.addEventListener("orientationchange", this.resizeEvent, false);
            this.resizeEvent();
        }

        onOpenMetersModalData()
        {
            //modalTranslateData.el = this.$refs.open_meters_button.$el;
            this.metersDataModalIsOpened = !this.metersDataModalIsOpened;
        }

    }
</script>