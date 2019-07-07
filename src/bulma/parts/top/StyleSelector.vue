<template>
    <core-style-selector>
        <template v-slot:default="{ styles, hasStyle, optionEvents }">
            <dropdown class="style-selector"
                manual>
                <template v-slot:label>
                    <span class="icon is-small">
                        <fa icon="table"/>
                    </span>
                </template>
                <template v-slot:options>
                    <a v-for="(style, key) in styles"
                        :key="key"
                        class="dropdown-item rounded-sm block py-1 px-1
                                whitespace-no-wrap w-full text-center
                                cursor-pointer no-underline relative text-sm hover:bg-white-smoke"
                        :class="{ 'is-active bg-blue-500 hover:bg-blue-400 font-semibold text-white': hasStyle(style) }"
                        v-on="optionEvents(style)">
                        {{ key }}
                    </a>
                </template>
            </dropdown>
        </template>
    </core-style-selector>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core';
import { faTable } from '@fortawesome/free-solid-svg-icons';
import Dropdown from '@enso-ui/dropdown/bulma';
import CoreStyleSelector from '../../../renderless/parts/top/CoreStyleSelector.vue';

library.add(faTable);

export default {
    name: 'StyleSelector',

    components: { CoreStyleSelector, Dropdown },
};
</script>

<style lang="scss">
    .vue-table .style-selector {
        .dropdown-item {
            padding: .5em .8em;
        }

        .button .icon:first-child:not(:last-child) {
            margin: unset;
        }
    }
</style>
