<template>
    <div class="sub-page-area">
        <v-breadcrumbs :items="breadcrumbs">
            <template v-slot:item="{ item }">
                <v-breadcrumbs-item v-if="item && item.text" :href="item.href" :disabled="item.disabled">
                    {{ item.text.toUpperCase() }}
                </v-breadcrumbs-item>
            </template>
        </v-breadcrumbs>
        <v-container>
            <v-card class="elevation-0">
                <v-card-title>
                    <h2>{{ item.title }}</h2>
                </v-card-title>
                <v-card-text class="text--primary">
                    <v-row no-gutters>
                        <v-col cols="10">
                            <div class="description-area">{{ item.description }}</div>
                        </v-col>
                        <v-col cols="2">
                            <v-card class="elevation-0" style="border: 1px solid #000;" width="100%" height="100%">
                                <v-card-text class="text--primary">
                                    <p>ID: {{ item.id }}</p>
                                    <p>Created: {{ item.created }}</p>
                                    <p>Last Modified: {{ item.updated }}</p>
                                </v-card-text>
                            </v-card>
                        </v-col>
                    </v-row>
                </v-card-text>
                <v-card-text class="text--primary">
                    <div class="techniques-table-area">
                        <h2>Techniques</h2>
                        <v-simple-table>
                            <template v-slot:default>
                                <thead>
                                    <tr>
                                        <th class="text-left">
                                            ID
                                        </th>
                                        <th class="text-left">
                                            NAME
                                        </th>
                                        <th class="text-left">
                                            Description
                                        </th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="(subItem, index) in item.items" :key="index" style="cursor: pointer;" @click="() => $router.push({
                                        name: 'techniques-tactic-technique',
                                        params: {
                                            tactic: item.to.replace('/', ''),
                                            technique: subItem.to.replace('/', '')
                                        }
                                    })">
                                        <td>{{ subItem.id }}</td>
                                        <td>{{ subItem.title }}</td>
                                        <td>{{ subItem.description }}</td>
                                    </tr>
                                </tbody>
                            </template>
                        </v-simple-table>
                    </div>
                </v-card-text>
            </v-card>
        </v-container>
    </div>
</template>
<script>
import data from '~/static/matrix.json'
export default {
    data() {
        return {
            item: {},
        };
    },
    computed: {
        breadcrumbs() {
            const _default = [{
                text: 'Home',
                disabled: false,
                href: '/',
            },
            {
                text: 'Tactics',
                disabled: false,
                href: '/tactics',
            }]
            const _data = data.items.filter(x => x.to === "/" + this.$route.params.tactic)
            if (_data && _data.length > 0) {
                this.item = _data[0];
                return [
                    ..._default,
                    {
                        text: this.item.title,
                        disabled: true,
                        href: `/tactics/${this.$route.params.tactic}`,
                    }
                ]
            }
            return _default
        }
    },
};
</script>

<style lang="scss" scoped>
.sub-page-area {
    display: flex;
    flex: 1;
    flex-direction: column;
}

.techniques-table-area {
    margin-top: 50px;
}

p {
    margin-bottom: 0px;
}
</style>