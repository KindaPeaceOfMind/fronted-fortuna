<style scoped lang="scss">
    @import "../../stylesheets/kira-fonts";

</style>

<template>
    <successable-modal-component :is-enabled="isOpened" :mode="currentMode" @close="$emit('close')">
        <template v-slot:title>Передать показания</template>
        <template v-slot:main>
            <meters-data-body-component @start-process="currentMode = 'loading'"
                                        @success-process="currentMode = 'success'" />
        </template>
        <template v-slot:success_text>Отличные показания!</template>
    </successable-modal-component>
</template>

<script>
    import { Options, Vue } from "vue-class-component";

    import SuccessableModalComponent from '../modal_types/SuccessableModalComponent';
    import MetersDataBodyComponent from "../modal_bodys/MetersDataBodyComponent";

    const Component = Options;
    @Component({
        components: {
            SuccessableModalComponent,
            MetersDataBodyComponent
        },
        props: {
            isOpened: Boolean
        },
        watch: {
            isOpened: function(newVal) {
                if(newVal) {
                    this.currentMode = 'enter';
                }
            }
        },
        emits: ['close']
    })
    export default class MetersDataModalComponent extends Vue
    {
        currentMode = 'enter';

    }
</script>
