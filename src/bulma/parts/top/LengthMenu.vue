<template>
    <core-length-menu>
        <template v-slot:default="{ isActive, optionEvents }">
            <dropdown class="length-menu"
                width="4em">
                <template v-slot:label>
                    {{ state.meta.length }}
                </template>
                <template v-slot:options>
                    <a v-for="value in state.template.lengthMenu"
                        :key="value"
                        class="dropdown-item rounded-sm block py-1 px-1
                                whitespace-no-wrap w-full text-center
                                cursor-pointer no-underline relative text-sm hover:bg-white-smoke"
                        :class="{ 'is-active bg-blue-500 hover:bg-blue-400 font-semibold text-white': isActive(value) }"
                        v-on="optionEvents(value)">
                        {{ value }}
                    </a>
                </template>
            </dropdown>
        </template>
    </core-length-menu>
</template>

<script>
import Dropdown from '@enso-ui/dropdown/bulma';
import CoreLengthMenu from '../../../renderless/parts/top/CoreLengthMenu.vue';

export default {
    name: 'LengthMenu',

    components: { CoreLengthMenu, Dropdown },

    inject: ['state'],
};
</script>

<style lang="scss">
    .vue-table .length-menu {
        .dropdown-item {
            padding: .5em 1.7em;
        }
    }
</style>
