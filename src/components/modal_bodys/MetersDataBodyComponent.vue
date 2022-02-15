<style scoped lang="scss">
    @import "../../stylesheets/kira-fonts";

    .v-input-form
    {
        width: auto;
    }

    .v-send-button
    {
        text-align: center;
    }

    .v-send-text
    {
        width: 200px;
    }

    .v-no-break
    {
        white-space: nowrap;
    }

    .v-sub-title
    {
        text-align: left;
        margin-bottom: 16px;
        color: var(--kr-color-layout-black-metallic);
    }

    @media (max-width: 680px)
    {
        .v-send-button
        {
            width: 100%;
        }

        .v-send-text
        {
            width: unset;
        }
    }
</style>

<template>
    <simple-form-group-fragment>
        <simple-form-row-group-fragment>
            <kr-form-default-input-component class="v-input-form"
                                             :krForm="krForm"
                                             :krFormData="requestData"
                                             field="streetHouse"
                                             name="street"
                                             autocomplete="street-address"
            >Улица и дом</kr-form-default-input-component>
            <simple-form-kr-form-errors-fragment
                    :data="requestData"
                    :fields="[ 'streetHouse' ]"
            />
        </simple-form-row-group-fragment>

        <simple-form-row-group-fragment>
            <simple-form-row-triple-fragment>
                <kr-form-default-input-component class="v-input-form"
                                                 :krForm="krForm"
                                                 :krFormData="requestData"
                                                 field="apartment"
                                                 name="apartment"
                >
                    <template v-if="lowModeEnabled">Кв.</template>
                    <template v-else>Квартира</template>
                </kr-form-default-input-component>

                <kr-form-default-input-component class="v-input-form"
                                                 :krForm="krForm"
                                                 :krFormData="requestData"
                                                 field="entrance"
                                                 name="entrance"
                >
                    <template v-if="lowModeEnabled">Под.</template>
                    <template v-else>Подъезд</template>
                </kr-form-default-input-component>

                <kr-form-default-input-component class="v-input-form"
                                                 :krForm="krForm"
                                                 :krFormData="requestData"
                                                 field="floor"
                                                 name="floor"
                >Этаж</kr-form-default-input-component>
            </simple-form-row-triple-fragment>

            <simple-form-kr-form-errors-fragment
                    :data="requestData"
                    :fields="[ 'apartment', 'entrance', 'floor' ]"
            />
        </simple-form-row-group-fragment>
    </simple-form-group-fragment>

    <simple-form-group-fragment>
        <simple-form-row-group-fragment>
            <kr-form-default-input-component class="v-input-form"
                                             :krForm="krForm"
                                             :krFormData="requestData"
                                             field="name"
                                             name="name"
                                             autocomplete="name"
            >Ваше ФИО</kr-form-default-input-component>
            <simple-form-kr-form-errors-fragment
                    :data="requestData"
                    :fields="[ 'name' ]"
            />
        </simple-form-row-group-fragment>

        <simple-form-row-group-fragment>
            <simple-form-row-double-fragment>
                <kr-form-default-input-component class="v-input-form"
                                                 :krForm="krForm"
                                                 :krFormData="requestData"
                                                 field="phoneNumber"
                                                 type="tel"
                                                 name="tel"
                                                 autocomplete="tel"

                                                 :imask-options="phoneMask"
                >Телефон</kr-form-default-input-component>

                <kr-form-default-input-component class="v-input-form"
                                                 :krForm="krForm"
                                                 :krFormData="requestData"
                                                 field="email"
                                                 type="email"
                                                 name="email"
                                                 autocomplete="email"

                >E-mail</kr-form-default-input-component>
            </simple-form-row-double-fragment>

            <simple-form-kr-form-errors-fragment
                    :data="requestData"
                    :fields="[ 'phoneNumber', 'email' ]"
            />
        </simple-form-row-group-fragment>
    </simple-form-group-fragment>

    <simple-form-group-fragment>
        <kr-form-default-input-component class="v-input-form"
                                         :krForm="krForm"
                                         :krFormData="requestData"
                                         field="personalAccountNumber"
                                         :imask-options="personalAccountNumberMask"
                                         type="number"
                                         name="account_number"
        >Лицевой счет</kr-form-default-input-component>
        <simple-form-kr-form-errors-fragment
                :data="requestData"
                :fields="[ 'personalAccountNumber' ]"
        />
    </simple-form-group-fragment>

    <simple-form-group-fragment>
        <div class="v-sub-title kr-font-h4">Холодная вода (куб. м)</div>

        <simple-form-row-group-fragment v-for="index in coldWaterCount" :key="requestData[`coldWater_${index}_place`]">
            <simple-form-row-double-second-long-fragment>
                <kr-form-default-input-component class="v-input-form"
                                                 :krForm="krForm"
                                                 :krFormData="requestData"
                                                 :field="`coldWater_${index}_place`"
                                                 name="coldWater_place"

                                                 @change="onChangeMeter('coldWater', index, 'place')"
                                                 @input="onInputMeter('coldWater', index, 'place')"

                >Счетчик</kr-form-default-input-component>

                <kr-form-default-input-component class="v-input-form"
                                                 :krForm="krForm"
                                                 :krFormData="requestData"
                                                 :field="`coldWater_${index}_value`"

                                                 @change="onChangeMeter('coldWater', index, 'value')"
                                                 @input="onInputMeter('coldWater', index, 'value')"

                                                 :imask-options="valueMeterMask"
                >Показание</kr-form-default-input-component>
            </simple-form-row-double-second-long-fragment>

            <simple-form-kr-form-errors-fragment
                    :data="requestData"
                    :fields="[ `coldWater_${index}_place`, `coldWater_${index}_value` ]"
            />
        </simple-form-row-group-fragment>


    </simple-form-group-fragment>

    <simple-form-group-fragment>
        <div class="v-sub-title kr-font-h4">Горячая вода (куб. м)</div>

        <simple-form-row-group-fragment v-for="index in hotWaterCount" :key="requestData[`hotWater_${index}_place`]">
            <simple-form-row-double-second-long-fragment>
                <kr-form-default-input-component class="v-input-form"
                                                 :krForm="krForm"
                                                 :krFormData="requestData"
                                                 :field="`hotWater_${index}_place`"
                                                 name="hotWater_place"

                                                 @change="onChangeMeter('hotWater', index, 'place')"
                                                 @input="onInputMeter('hotWater', index, 'place')"

                >Счетчик</kr-form-default-input-component>

                <kr-form-default-input-component class="v-input-form"
                                                 :krForm="krForm"
                                                 :krFormData="requestData"
                                                 :field="`hotWater_${index}_value`"

                                                 @change="onChangeMeter('hotWater', index, 'value')"
                                                 @input="onInputMeter('hotWater', index, 'value')"

                                                 :imask-options="valueMeterMask"

                >Показание</kr-form-default-input-component>
            </simple-form-row-double-second-long-fragment>

            <simple-form-kr-form-errors-fragment
                    :data="requestData"
                    :fields="[ `hotWater_${index}_place`, `hotWater_${index}_value` ]"
            />
        </simple-form-row-group-fragment>
    </simple-form-group-fragment>

    <simple-form-group-fragment>
        <default-checkbox-component
                :checked="requestData.agreeProcess.value"
                @change="krForm.trySetInput('agreeProcess', $event)"
                :is-error="requestData.agreeProcess.errors.length > 0">Даю согласие на обработку моих <a href="#" @click="krForm.trySetInput('agreeProcess', !requestData.agreeProcess.value)" class="v-no-break">персональных данных</a></default-checkbox-component>
        <simple-form-kr-form-errors-fragment
                :data="requestData"
                :fields="[ `agreeProcess` ]"
        />
    </simple-form-group-fragment>

    <flex-button-component @action="send" class="v-send-button" mode="text-only">
        <template v-slot:text>
            <div class="v-send-text">Отправить</div>
        </template>
    </flex-button-component>
</template>

<script>
    import { Options, Vue } from "vue-class-component";

    import CloseButtonComponent from '../CloseButtonComponent';
    import RandomLoaderSpinnerComponent from '../RandomLoaderSpinnerComponent';

    import ModalClosableTitledComponent from '../ModalClosableTitledComponent';

    import imaskRussianPhoneMask from '../../lib/imask/russian_phone_mask';

    import DefaultInputComponent from "../DefaultInputComponent";

    import DefaultTextAreaComponent from '../DefaultTextAreaComponent';

    import FlexButtonComponent from '../FlexButtonComponent';

    import DefaultCheckboxComponent from '../DefaultCheckboxComponent';

    import TradeRequestsManager from "../../lib/trade/TradeRequestsManager";

    import IconSuccessComponent from "../icons/IconSuccessComponent";

    import KrForm from "../../lib/krform/KrForm";
    import KrFormEmptyStringValidation from "@/lib/krform/validations/KrFormEmptyStringValidation";
    import KrFormLimitLengthPhoneValidation from "@/lib/krform/validations/KrFormLimitLengthPhoneValidation";
    import KrFormEmailValidation from "@/lib/krform/validations/KrFormEmailValidation";

    import KrFormDefaultInputComponent from '../forms/krform_simple/KrFormDefaultInputComponent';

    import SuccessModalBodyComponent from "../modal_bodys/SuccessModalBodyComponent";

    import 'imask/esm/masked/number';
    import SimpleFormGroupFragment from "@/components/forms/simple_fragments/SimpleFormGroupFragment";
    import SimpleFormRowGroupFragment from "@/components/forms/simple_fragments/SimpleFormRowGroupFragment";
    import SimpleFormRowTripleFragment from "@/components/forms/simple_fragments/SimpleFormRowTripleFragment";
    import SimpleFormRowDoubleFragment from "@/components/forms/simple_fragments/SimpleFormRowDoubleFragment";
    import SimpleFormRowDoubleSecondLongFragment
        from "@/components/forms/simple_fragments/SimpleFormRowDoubleSecondLongFragment";
    import SimpleFormKrFormErrorsFragment from "@/components/forms/simple_fragments/SimpleFormKrFormErrorsFragment";

    const Component = Options;
    @Component({
        components: {
            SimpleFormKrFormErrorsFragment,
            SimpleFormRowDoubleSecondLongFragment,
            SimpleFormRowDoubleFragment,
            SimpleFormRowTripleFragment,
            SimpleFormRowGroupFragment,
            SimpleFormGroupFragment,
            DefaultTextAreaComponent,
            CloseButtonComponent,
            DefaultInputComponent,
            FlexButtonComponent,
            DefaultCheckboxComponent,
            IconSuccessComponent,
            RandomLoaderSpinnerComponent,
            ModalClosableTitledComponent,
            KrFormDefaultInputComponent,
            SuccessModalBodyComponent
        },
        props: {
            isOpened: Boolean
        },
        watch: {
            isOpened: function(newVal) {
                if(newVal)
                {
                    this.krForm.initializeFromStorage();
                }
            }
        },
        emits: ['start-process', 'success-process']
    })
    export default class MetersDataBodyComponent extends Vue
    {
        requestData = {
            streetHouse: {
                value: 'ул. Флегонтова, ',
                defaultValue: 'ул. Флегонтова, ',
                errors: [],
                validations: [
                    new KrFormEmptyStringValidation('Улица и дом')
                ],
                type: String
            },
            apartment: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [
                    new KrFormEmptyStringValidation('Квартира')
                ],
                type: String
            },
            entrance: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [
                    new KrFormEmptyStringValidation('Подъезд')
                ],
                type: String
            },
            floor: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [
                    new KrFormEmptyStringValidation('Этаж')
                ],
                type: String
            },
            name: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [
                    new KrFormEmptyStringValidation('Ваше ФИО')
                ],
                type: String
            },
            phoneNumber: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [
                    new KrFormEmptyStringValidation('Телефон'),
                    new KrFormLimitLengthPhoneValidation(11)
                ],
                type: String
            },
            email: {
                value: '',
                errors: [],
                defaultValue: '',
                validations: [
                    new KrFormEmailValidation()
                ],
                type: String
            },
            personalAccountNumber: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [
                    new KrFormEmptyStringValidation('Лицевой счет')
                ],
                type: String
            },

            coldWater_1_place: {
                value: '№1 (кухня)',
                defaultValue: '№1 (кухня)',
                errors: [],
                validations: [],
                type: String
            },

            coldWater_1_value: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [],
                type: String
            },

            coldWater_2_place: {
                value: '№2 (туалет)',
                defaultValue: '№2 (туалет)',
                errors: [],
                validations: [],
                type: String
            },

            coldWater_2_value: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [],
                type: String
            },

            hotWater_1_place: {
                value: '№1 (кухня)',
                defaultValue: '№1 (кухня)',
                errors: [],
                validations: [],
                type: String
            },

            hotWater_1_value: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [],
                type: String
            },

            hotWater_2_place: {
                value: '№2 (туалет)',
                defaultValue: '№2 (туалет)',
                errors: [],
                validations: [],
                type: String
            },

            hotWater_2_value: {
                value: '',
                defaultValue: '',
                errors: [],
                validations: [],
                type: String
            },

            agreeProcess: {
                value: false,
                defaultValue: false,
                errors: [],
                validations: [
                    {
                        errorText: 'Согласие необходимо для отправки заявки',
                        isValid: function (value) {
                            return value;
                        }
                    }
                ],
                type: Boolean
            }
        }

        krForm = new KrForm('requestModalForm-', this.requestData);

        lowModeEnabled = false;

        coldWaterCount = 2;
        hotWaterCount = 2;

        beforeMount()
        {
            this.lowModeQuery = window.matchMedia('(max-width: 400px)');

            this.onInputMeter("coldWater", 1, 'value');
            this.onInputMeter("hotWater", 1, 'value');

            window.addEventListener("resize", this.resizeEvent, false);
            window.addEventListener("orientationchange", this.resizeEvent, false);
            this.resizeEvent();
        }

        beforeUnmount()
        {
            window.removeEventListener("resize", this.resizeEvent, false);
            window.removeEventListener("orientationchange", this.resizeEvent, false);
        }

        onChangeMeter(meterName, indexMeter, typeField)
        {
            /*const meterCount = this[`${meterName}Count`];

            if(indexMeter !== meterCount)
            {
                if(this.requestData[`${meterName}_${indexMeter}_place`].value === '' &&
                    this.requestData[`${meterName}_${indexMeter}_value`].value === '')
                {
                    for(let i = indexMeter; i < meterCount; i++)
                    {
                        this.requestData[`${meterName}_${i}_place`] = this.requestData[`${meterName}_${i + 1}_place`];
                        this.requestData[`${meterName}_${i}_value`] = this.requestData[`${meterName}_${i + 1}_value`];
                    }

                    this[`${meterName}Count`]--;
                }
            }*/
        }

        onInputMeter(meterName, indexMeter, typeField)
        {
            /*if(indexMeter === this[`${meterName}Count`])
            {
                this[`${meterName}Count`]++;

                this.requestData[`${meterName}_${this[`${meterName}Count`]}_place`] = {
                    value: '',
                    defaultValue: '',
                    errors: [],
                    validations: [],
                    type: String
                };

                this.requestData[`${meterName}_${this[`${meterName}Count`]}_value`] = {
                    value: '',
                    defaultValue: '',
                    errors: [],
                    validations: [],
                    type: String
                };
            }*/
        }

        resizeEvent()
        {
            this.lowModeEnabled = this.lowModeQuery.matches;
        }

        async send()
        {
            if(!this.krForm.isValidForm())
            {
                return;
            }

            this.$emit('start-process');

            let description =
`Улица и дом: ${this.requestData.streetHouse.value}
Квартира: ${this.requestData.apartment.value}
Подъезд: ${this.requestData.entrance.value}
Этаж: ${this.requestData.floor.value}

ФИО: ${this.requestData.name.value}
Телефон: ${this.requestData.phoneNumber.value}
E-mail: ${this.requestData.email.value}

Лицевой счет: ${this.requestData.personalAccountNumber.value}

-- Холодная вода (куб. м) --`;

            for (let i = 1; i <= this.coldWaterCount; i++)
            {
                description += '\n';

                if(i === 1)
                {
                    description += '-\n';
                }

                description +=
`Счетчик: ${this.requestData[`coldWater_${i}_place`].value}
Показание: ${this.requestData[`coldWater_${i}_value`].value}
-`;
            }

            description += `

-- Горячая вода (куб. м) --`;

            for (let i = 1; i <= this.hotWaterCount; i++)
            {
                description += '\n';

                if(i === 1)
                {
                    description += '-\n';
                }

                description +=
`Счетчик: ${this.requestData[`hotWater_${i}_place`].value}
Показание: ${this.requestData[`hotWater_${i}_value`].value}
-`;
            }

            await TradeRequestsManager.create({
                contractor_name: this.requestData.name.value,
                contractor_phonenumber: this.requestData.phoneNumber.value,
                description: description
            });

            //this.krForm.clearFormDataFromLocalStorage();
            //this.krForm.setDefaultValues();

            this.krForm.trySetInput("coldWater_1_value", "");
            this.krForm.trySetInput("coldWater_2_value", "");
            this.krForm.trySetInput("hotWater_1_value", "");
            this.krForm.trySetInput("hotWater_2_value", "");
            this.krForm.trySetInput("agreeProcess", false);

            this.$emit('success-process');
        }

        phoneMask = imaskRussianPhoneMask;

        valueMeterMask = {
            mask: Number,  // enable number mask

            // other options are optional with defaults below
            scale: 9,  // digits after point, 0 for integers
            signed: false,  // disallow negative
            thousandsSeparator: '',  // any single char
            padFractionalZeros: false,  // if true, then pads zeros at end to the length of scale
            normalizeZeros: true,  // appends or removes zeros at ends
            radix: ',',  // fractional delimiter
            mapToRadix: ['.'],  // symbols to process as radix
        }

        personalAccountNumberMask = {
            mask: Number,
            scale: 0,
            signed: false
        }
    }
</script>
