<style scoped lang="scss">
    @import "../stylesheets/kira-fonts";

    .vc-flex-button
    {
        display: inline-block;
        box-sizing: border-box;

        color: var(--kr-color-main-white);

        background: var(--kr-color-feedback-active-2);
        border-radius: 8px;

        user-select: none;

        cursor: pointer;

        -webkit-tap-highlight-color: transparent;

        padding: 14px 16px;

        &:hover
        {
            background: var(--kr-color-feedback-active-1);
        }

        &:active
        {
            background: var(--kr-color-feedback-active-3);
        }

        &.vc-flex-button-disabled
        {
            cursor: unset;
            background: var(--kr-color-feedback-inactive);
        }
    }

    .v-text
    {
        display: inline-block;

        vertical-align: top;
    }

    .v-icon-btn
    {
        display: inline-block;

        margin-right: 8px;

        vertical-align: top;
    }

    .vc-flex-button-text-only
    {
        &.vc-flex-button
        {
            padding: 14px 20px;
        }

        .v-icon-btn
        {
            display: none;
        }
    }

    .vc-flex-button-icon-only
    {
        &.vc-flex-button
        {
            padding: 14px 14px;
        }

        .v-text
        {
            display: none;
        }

        .v-icon-btn
        {
            margin-right: 0;
        }
    }
</style>

<template>
    <a class="vc-flex-button"

       @click="onClick"
       @keyup="onKeyUp"

       :tabindex="enabled ? '0' : undefined "
       :class="{
        'vc-flex-button-full': mode === 'full',
        'vc-flex-button-text-only': mode === 'text-only',
        'vc-flex-button-icon-only': mode === 'icon-only',
        'vc-flex-button-disabled': !enabled
    }">
        <div class="v-icon-btn">
            <slot name="icon" />
        </div>
        <div class="v-text kr-font-button">
            <slot name="text" />
        </div>
    </a>
</template>

<script>
    import { Options, Vue } from "vue-class-component";

    import IconArtComponent from "./icons/IconArtComponent"

    const Component = Options;
    @Component({
        components: {

        },
        props: {
            to: String,
            mode: {
                type: String,
                default: 'full'
            },
            enabled: {
                type: Boolean,
                default: true
            }
        },
        emits: [ 'action' ]
    })
    export default class FlexButtonComponent extends Vue {
        onClick()
        {
            if(this.enabled)
            {
                this.$emit('action');
            }
        }

        onKeyUp(e)
        {
            if(!this.enabled)
                return;

            if (e.keyCode === 13) {
                this.$emit('action');
                e.preventDefault();
            }
        }
    }
</script>