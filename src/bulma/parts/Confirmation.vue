<template>
    <modal show
        @close="closeConfirmation">
        <!-- <div class="box"> -->
        <div class="box w-5/6 sm:w-2/3 m-auto">
            <!-- <h5 class="subtitle is-5"> -->
            <h5 class="subtitle is-5
            text-xl mb-6 font-normal leading-tight text-gray-290">
                {{ i18n(state.action.button.message || "Are you sure?") }}
            </h5>
            <hr>
            <!-- <div class="level"> -->
            <div class="flex">
                <!-- <div class="level-left"/> -->
                <!-- <div class="level-right"> -->
                    <!-- <div class="level-item"> -->
                    <div class="ltr:ml-auto rtl:mr-auto">
                        <button class="button is-outlined h-9"
                            @click="closeConfirmation">
                            {{ i18n("Cancel") }}
                        </button>
                        <!-- <button class="button is-danger has-margin-left-small" -->
                        <button class="button is-danger
                        bg-red-500 text-white border-red-400 hover:border-red-700 hover:text-white hover:bg-red-600
                        focus:border-transparent focus:text-white focus:shadow-outlineRed h-9"
                            v-focus
                            @click="doButtonAction">
                            {{ i18n("Yes") }}
                        </button>
                    </div>
                <!-- </div> -->
            </div>
        </div>
    </modal>
</template>

<script>
import { focus } from '@enso-ui/directives';
import { Modal } from '@enso-ui/modal/bulma';

export default {
    name: 'Confirmation',

    components: { Modal },

    directives: { focus },

    inject: ['state', 'i18n', 'closeConfirmation', 'doButtonAction'],
};
</script>
