<template>
    <div class="sub-page">
        <v-navigation-drawer permanent>
            <v-list-item>
                <v-list-item-content>
                    <v-list-item-title class="text-h6">
                        TECHNIQUES
                    </v-list-item-title>
                </v-list-item-content>
            </v-list-item>
            <v-divider></v-divider>
            <v-list>
                <v-list-group v-for="item in items" :key="item.title" v-model="item.active" no-action>
                    <template v-slot:activator>
                        <v-list-item-content>
                            <v-list-item-title>{{ item.title }}</v-list-item-title>
                        </v-list-item-content>
                    </template>

                    <v-list-item v-for="child in item.items" :key="child.title" style="padding-left: 35px;" :to="'/techniques' + item.to + child.to">
                        <v-list-item-content>
                            <v-list-item-title>{{ child.title }}</v-list-item-title>
                        </v-list-item-content>
                    </v-list-item>
                </v-list-group>
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