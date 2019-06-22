<template>
    <core-controls>
        <template v-slot:default="{
                reloadEvents, resetEvents, forceInfoEvents, controlBindings, controlEvents,
                searchBindings, searchEvents, clearEvents
            }">
            <!-- <div class="top-controls has-background-light"> -->
            <div class="top-controls has-background-light bg-white-smoke">
                <!-- <div class="columns is-multiline"> TODO:if not working properly for -m-3 separate -mb-3 for last child -->
                <div class="columns is-multiline flex flex-wrap -m-3">
                    <!-- <div class="column table-controls is-half-tablet is-one-third-desktop has-text-centered-mobile has-padding-small"> -->
                    <div class="column table-controls is-half-tablet is-one-third-desktop has-text-centered-mobile has-padding-small
                     block w-full sm:w-1/2 lg:w-1/3 text-center sm:ltr:text-left sm:rtl:text-right p-1">
                        <length-menu v-if="state.template.controls.includes('length')"/>
                        <column-visibility v-if="state.template.controls.includes('columns')"/>
                        <!-- <style-selector class="is-hidden-mobile" -->
                        <style-selector class="is-hidden-mobile hidden md:inline-flex"
                            v-if="state.template.controls.includes('style')"/>
                        <!-- <a class="button" -->
                        <a class="button rounded text-gray-290 text-center
                            items-center justify-center p-2 h-9 inline-flex border border-gray-860
                             truncate cursor-pointer flex-1 bg-white hover:border-gray-480"
                            v-on="reloadEvents"
                            v-if="state.template.controls.includes('reload')">
                            <span class="icon is-small">
                                <fa icon="sync"/>
                            </span>
                        </a>
                        <!-- <a class="button" -->
                        <a class="button rounded text-gray-290 text-center
                            items-center justify-center p-2 h-9 inline-flex border border-gray-860
                             truncate cursor-pointer flex-1 bg-white hover:border-gray-480"
                            v-on="resetEvents"
                            v-if="state.template.controls.includes('reset')">
                            <span class="icon is-small">
                                <fa icon="undo"/>
                            </span>
                        </a>
                        <!-- <a class="button" -->
                        <a class="button rounded text-gray-290 text-center
                            items-center justify-center p-2 h-9 inline-flex border border-gray-860
                             truncate cursor-pointer flex-1 bg-white hover:border-gray-480"
                            v-on="forceInfoEvents"
                            v-if="!state.body.fullRecordInfo">
                            <!-- <span class="icon is-small has-text-info"> -->
                            <span class="icon is-small has-text-info text-blue-400">
                                <fa icon="info-circle"/>
                            </span>
                        </a>
                    </div>
                    <!-- <div class="column table-buttons is-one-third-desktop is-half-tablet has-text-right-tablet has-text-centered-mobile has-padding-small" -->
                    <div class="column table-buttons is-one-third-desktop is-half-tablet has-text-right-tablet has-text-centered-mobile has-padding-small
                    block w-full sm:w-1/2 lg:w-1/3 text-center sm:rtl:text-left sm:ltr:text-right p-1"
                        v-if="state.template.buttons">
                            <!-- class="button has-margin-left-small" -->
                        <a v-for="button in state.template.buttons.global"
                            class="button has-margin-left-small rounded text-gray-290 text-center
                            items-center justify-center py-2 px-3 h-9 inline-flex border border-gray-860
                             truncate cursor-pointer flex-1 bg-white hover:border-gray-480"
                            :class="button.class"
                            :key="button.label"
                            v-bind="controlBindings(button)"
                            v-on="controlEvents(button)">
                            <span class="is-hidden-mobile hidden md:block">
                                {{ i18n(button.label) }}
                            </span>
                            <span class="icon is-small">
                                <fa :icon="button.icon"/>
                            </span>
                            <span class="is-hidden-mobile hidden md:block"/>
                        </a>
                    </div>
                    <!-- <div class="column has-padding-small is-one-third-desktop search-input"> -->
                    <div class="column has-padding-small is-one-third-desktop search-input
                     block w-full lg:w-1/3 p-1">
                        <!-- <p class="control has-icons-left has-icons-right" -->
                        <p class="control has-icons-left has-icons-right
                        relative ltr:text-left rtl:text-right flex content-center"
                            v-if="state.meta.searchable">
                            <!-- <input class="input has-text-centered is-rounded" -->
                            <input class="input has-text-centered is-rounded
                            px-10  w-full block bg-white h-9 rounded-full
                        border border-gray-860 shadow-inner focus:shadow-outline hover:border-gray-500 hover:shadow text-base"
                                type="text"
                                v-bind="searchBindings"
                                v-on="searchEvents"
                                :placeholder="i18n('Search')">
                            <!-- <span class="icon is-small is-left"> -->
                            <span class="items-center inline-flex justify-center
                        absolute top-0 ltr:left-0 rtl:right-0
                        text-gray-500 w-10 h-9">
                                <fa icon="search"/>
                            </span>
                            <!-- <span class="icon is-small is-right clear-button" -->
                            <span class="items-center inline-flex justify-center
                        absolute top-0 rtl:left-0 ltr:right-0
                        focus:text-gray-480 text-gray-500 w-10 h-9"
                                v-if="state.meta.search && !state.meta.loading"
                                v-on="clearEvents">
                                <a class="delete is-small"/>
                            </span>
                        </p>
                    </div>
                </div>
            </div>
        </template>
    </core-controls>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core';
import {
    faSync, faUndo, faSearch, faInfoCircle,
} from '@fortawesome/free-solid-svg-icons';
import CoreControls from '../../../renderless/parts/top/CoreControls.vue';
import LengthMenu from './LengthMenu.vue';
import ColumnVisibility from './ColumnVisibility.vue';
import StyleSelector from './StyleSelector.vue';

library.add(faSync, faUndo, faSearch, faInfoCircle);

export default {
    name: 'TopControls',

    components: {
        CoreControls, LengthMenu, ColumnVisibility, StyleSelector,
    },

    inject: ['state', 'i18n'],
};
</script>

<style lang="scss">
    .vue-table .top-controls {
        border-top-left-radius: inherit;
        border-top-right-radius: inherit;
        padding: 1em;

        .control.has-icons-right .icon.clear-button {
            pointer-events: all;
        }

        @media screen and (min-width: 1024px) {
            .table-controls {
                order: 1;
            }

            .search-input {
                order: 2;
            }

            .table-buttons {
                order: 3;
            }
        }
    }
</style>
