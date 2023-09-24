<template>
    <div class="sub-page">
        <v-navigation-drawer permanent>
            <v-list-item>
                <v-list-item-content>
                    <v-list-item-title class="text-h6">
                        TACTICS
                    </v-list-item-title>
                </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
            <v-list light>
                <v-list-item v-for="item in items" :key="item.title" link :to="'/tactics' + item.to">
                    <v-list-item-content>
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>
        <NuxtChild />
    </div>
</template>
<script>
import { items } from '~/static/matrix.json'
export default {
    data() {
        return {
            items: [],
        };
    },
    created() {
        this.items = items;
    }
};
</script>
<style lang="scss" scoped>
.sub-page {
    height: 100%;
    display: flex;
}
</style>