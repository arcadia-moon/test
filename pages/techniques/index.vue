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
                    <h2>Techniques</h2>
                </v-card-title>
                <v-card-text class="text--primary">
                    <div class="description-area">{{ item.techniques.description }}</div>
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
                                <tr v-for="(item, index) in items" :key="index" style="cursor: pointer;"
                                    @click="() => $router.push(item._to)">
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
      title: `TECHNIQUE`,
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
                text: 'Techniques',
                disabled: true,
                href: '/techniques',
            }]
        };
    },
    computed: {
        items() {
            const data = []
            if (this.item && this.item.items) {
                for (const _item of this.item.items) {
                    for (const __item of _item.items) {
                        data.push(Object.assign(__item, {
                            _to: {
                                name: "techniques-tactic-technique",
                                params: {
                                    tactic: _item.to.replace("/", ""),
                                    technique: __item.to.replace("/", "")
                                }
                            }
                        }))
                    }
                }
            }
            return data
        }
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