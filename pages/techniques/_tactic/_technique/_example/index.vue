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
                    <h2>{{ example.title }}</h2>
                </v-card-title>
                <v-card-text class="text--primary">
                    <v-row no-gutters>
                        <v-col cols="10">
                            <div class="description-area">{{ example.description }}</div>
                        </v-col>
                        <v-col cols="2">
                            <v-card class="elevation-0" style="border: 1px solid #000;" width="100%" height="100%">
                                <v-card-text class="text--primary">
                                    <p>ID: {{ example.id }}</p>
                                    <p>Created: {{ example.created }}</p>
                                    <p>Last Modified: {{ example.updated }}</p>
                                </v-card-text>
                            </v-card>
                        </v-col>
                    </v-row>
                </v-card-text>

                <v-card-text class="text--primary" v-if="samples">
                    <div class="techniques-table-area">
                        <h2 style="margin-bottom: 5px;">Samples</h2>
                        <div class="markdown-body" v-html="samples"></div>
                    </div>
                </v-card-text>
                <v-card-text class="text--primary" v-if="example.reference && example.reference.length > 0">
                    <div class="techniques-table-area">
                        <h2>Reference</h2>
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
                                    <tr v-for="(reference, index) in example.reference" :key="index"
                                        style="cursor: pointer;">
                                        <td>{{ reference.id }}</td>
                                        <td>{{ reference.name }}</td>
                                        <td><a :href="reference.link" target="_blank" rel="noopener noreferrer">{{
                                            reference.link }}</a></td>
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
    head: {
      title: `EXAMPLE - ${this.$route.params.example}`,
    },
    data() {
        return {
            item: {},
            subItem: {},
            example: {},
            samples: ""
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
                text: 'Techniques',
                disabled: false,
                href: '/techniques',
            }]
            const _data = data.items.filter(x => x.to === "/" + this.$route.params.tactic)
            if (_data && _data.length > 0) {
                this.item = _data[0];
                const __data = this.item.items.filter(x => x.to === "/" + this.$route.params.technique)
                if (__data && __data.length > 0) {
                    this.subItem = __data[0];
                    const ___data = this.subItem.examples.filter(x => x.to === "/" + this.$route.params.example)
                    if (___data && ___data.length > 0) {
                        this.example = ___data[0];
                        try {
                            this.samples = require(`~/static/example/${this.example.id}.md`).default
                        }
                        catch {

                        }
                        return [
                            ..._default,
                            {
                                text: this.item.title,
                                disabled: false,
                                href: `/tactics/${this.$route.params.tactic}`,
                            },
                            {
                                text: this.subItem.title,
                                disabled: false,
                                href: `/techniques/${this.$route.params.tactic}/${this.$route.params.technique}`,
                            },
                            {
                                text: this.example.title,
                                disabled: true,
                                href: `/techniques/${this.$route.params.tactic}/${this.$route.params.technique}/${this.$route.params.example}`,
                            }
                        ]
                    }
                }
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

p {
    margin-bottom: 0px;
}
</style>