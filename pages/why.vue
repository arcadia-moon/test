<template>
    <v-container>
        <div class="markdown-body" v-html="require(`~/assets/why-header.md`).default"></div>
        <h2>QnA</h2>
        <v-row no-gutters>
            <v-alert v-for="(item, index) in qna" :key="index" :value="true" icon="mdi-information" :color="item.color"
                class="white--text">
                <h2>{{ item.q }}</h2>
                <h5>{{ item.a }}</h5>
            </v-alert>
        </v-row>
        <h2>Reference</h2>
        <v-row no-gutters>
            <li v-for="(item, index) in reference" :key="index">{{ item.text }}</li>
        </v-row>
    </v-container>
</template>

<script>
export default {
    head: {
      title: `WHY`,
    },
    data() {
        return {
            qna: [{
                "q": "1. Why was there no smart contract TTP matrix?",
                "a": "Smart contracts, fundamental components of blockchain platforms, are designed to facilitate transparent, irreversible transactions and agreements autonomously, contrasting with the malicious intentions often found in typical cyber-attack vectors. However, their unique, constrained application and divergent threat landscape, primarily focusing on the integrity and security of the contractual code and governed assets, present distinctive challenges, rendering the development of a specialized Tactics, Techniques, and Procedures (TTP) matrix a complex endeavor. The rapid evolution and the lack of standardization in smart contract fields, coupled with the prioritization of addressing more immediate and prevalent threats, have possibly delayed the establishment of a specialized and universally applicable TTP matrix for smart contracts.",
                "color": "#5cb85c"
            }, {
                "q": "2. How is it made?",
                "a": "Troy, a doctoral candidate researching Blockchain, Malware, and the MITRE ATT&CK Matrix, developed this framework. Troy has studied the potential of the ATT&CK matrix not only for preventing cyber-attacks but also for classifying campaigns and substantiating the possibilities in cyber attribution. He has developed this specific framework to demonstrate whether it is applicable and provable on a new platform like blockchain, pushing the boundaries of existing knowledge in insightful ways.",
                "color": "#5cb85c"
            }],
            reference: [{
                text: "You can help contribute to ATT&CK.",
                link: "http://naver.com"
            }]
        };
    },
};
</script>
<style lang="scss" scoped>
.profile-info {
    padding-left: 15px;
}
</style>