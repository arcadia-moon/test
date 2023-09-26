<template>
    <div class="full-page">
    <v-container>
        <v-row no-gutters align="center" justify="center">
            <v-col align="center" justify="center">
                <v-row style="justify-content: center;">
                    <v-avatar size="200">
                        <v-img :src="require(`~/assets/profile.jpeg`)"></v-img>
                    </v-avatar>
                </v-row>
                <v-row style="justify-content: center;">
                    <div class="profile-info">
                        <h3>Kyongmin Kim</h3>
                        <h5>Korea University</h5>
                    </div>
                </v-row>
            </v-col>
            <v-col>
                <div class="markdown-body" v-html="require(`~/assets/profile.md`).default"></div>
            </v-col>
        </v-row>

    </v-container>
    </div>
</template>

<script>
export default {
    head: {
      title: `PROFILE`,
    },
    data() {
        return {

        };
    },
};
</script>
<style lang="scss" scoped>
.profile-info {
    padding-left: 15px;
}
.full-page {
    display: flex;
    height: 100%;
    align-items: center;
}
</style>