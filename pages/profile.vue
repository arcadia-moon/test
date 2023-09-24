<template>
    <v-container>
        <v-row no-gutters align="center" justify="center">
            <div class="profile-img">
                <v-avatar size="100">
                    <v-img :src="require(`~/assets/profile.jpeg`)"></v-img>
                </v-avatar>
            </div>
            <div class="profile-info">
                <h3>Kyongmin Kim</h3>
                <h5>Korea University</h5>
            </div>
        </v-row>

        <h2>Contribute</h2>
        <v-row no-gutters>
            <p>You can help contribute to ATT&CK.</p>
            <p>ATT&CK is in a constant state of development. We are always on the lookout for new information to help refine
                and extend what is covered. If you have additional techniques, know about variations on one already covered,
                have examples of techniques in use, or have other relevant information, then we would like to hear from you.
            </p>
            <p>We are looking for contributions in the following areas in particular, but if you have other information you
                think may be useful, please reach us at attack@mitre.org.</p>
            <p>All contributions and feedback to ATT&CK are appreciated. Due to the high volume of contributions, it may
                take us about a week to get back to you. We may ask you follow-up questions to help us understand your
                contribution and gather additional information. We recommend you read our philosophy paper to understand our
                approach to maintaining ATT&CK so that we get the right details up front. If we find the contribution fills
                a gap, then we will make edits and send you a draft version of the technique or Group/Software page for your
                review prior to it being published, listing you as a contributor if desired. Content updates happen roughly
                every 6 months.</p>
        </v-row>
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
    data() {
        return {
            qna: [{
                "q": "You can help contribute to ATT&CK.",
                "a": "ATT&CK is in a constant state of development. We are always on the lookout for new information to help refine and extend what is covered. If you have additional techniques, know about variations on one already covered, have examples of techniques in use, or have other relevant information, then we would like to hear from you.",
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