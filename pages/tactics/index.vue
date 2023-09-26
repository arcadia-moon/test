<template>
    <div class="sub-page-area">
        <v-breadcrumbs :items="breadcrumbs">
            <template v-slot:item="{ item }">
                <v-breadcrumbs-item :href="item.href" :disabled="item.disabled">
                    {{ item.text.toUpperCase() }}
                </v-breadcrumbs-item>
            </template>
        </v-breadcrumbs>
        <v-container>
            <v-card class="elevation-0">
                <v-card-title>
                    <h2>Tactics</h2>
                </v-card-title>
                <v-card-text class="text--primary">
                    <div class="description-area">{{ item.tactics.description }}</div>
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
                                <tr v-for="(item, index) in item.items" :key="index" style="cursor: pointer;" @click="() => $router.push({
                                    name: 'tactics-tactic',
                                    params: {
                                        tactic: item.to.replace('/', ''),
                                    }
                                })">
                                    <td>{{ item.id }}</td>
                                    <td>{{ item.title }}</td>
                                    <td>{{ item.description }}</td>
                                </tr>
                            </tbody>
                        </template>
                    </v-simple-table>
                </v-card-text>
            </v-card>
        </v-container>
    </div>
</template>
<script>
import matrix from '~/static/matrix.json'
export default {
    head: {
      title: 'TACTIC',
    },
    data() {
        return {
            item: {},
            breadcrumbs: [{
                text: 'Home',
                disabled: false,
                href: '/',
            },
            {
                text: 'Tactics',
                disabled: true,
                href: '/tactics',
            }]
        };
    },
    created() {
        this.item = matrix;
    },
};
</script>

<style lang="scss" scoped>
.sub-page-area {
    display: flex;
    flex: 1;
    flex-direction: column;
}
.description-area {
    margin-bottom: 50px;
}
</style>