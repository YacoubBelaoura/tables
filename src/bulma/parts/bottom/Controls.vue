<template>
    <!-- <div class="columns is-gapless has-background-light bottom-controls"> -->
    <div class="columns is-gapless has-background-light bottom-controls
    flex bg-white-smoke justify-between flex-col sm:flex-row">
        <!-- <div class="column"> -->
        <div class="column block flex-1">
            <records-info/>
        </div>
        <!-- <div class="column is-narrow has-text-right"> -->
        <div class="column is-narrow has-text-right block ltr:text-right rtl:text-left">
            <pagination v-if="hasEntries()"/>
        </div>
    </div>
</template>

<script>

import RecordsInfo from './RecordsInfo.vue';
import Pagination from './Pagination.vue';

export default {
    name: 'BottomControls',

    components: { RecordsInfo, Pagination },

    inject: ['hasEntries'],
};

</script>

<style lang="scss">
    .vue-table .bottom-controls {
        border-bottom-left-radius: inherit;
        border-bottom-right-radius: inherit;
    }
</style>
