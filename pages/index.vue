<template>
  <div class="main">
    <v-row no-gutters class="matrix-item">
      <v-col v-for="(item, index) in items" :key="index" lg="1.5">
        <v-card class="elevation-0">
          <v-card-title class="matrix-title-area">
            <div class="matrix-title">{{ item.title }}</div>
            <div class="matrix-sub-title">{{ item.subTitle ?? "&nbsp;" }}</div>
            <div class="matrix-length">{{ item.items.length + 1 }} techniques</div>
          </v-card-title>
          <v-divider></v-divider>
          <v-list dense>
            <v-list-item v-for="(subItem, subIndex) in item.items" :key="subIndex">
              <v-list-item-content class="matrix-content" style="cursor: pointer;" @click="() => $router.push({
                name: 'techniques-tactic-technique',
                params: {
                  tactic: item.to.replace('/', ''),
                  technique: subItem.to.replace('/', '')
                }
              })">{{ subItem.title }}</v-list-item-content>
            </v-list-item>
          </v-list>
        </v-card>
      </v-col>
    </v-row>
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
.matrix-item {
  width: 100% !important;
  overflow-y: auto !important;
  flex-wrap: nowrap !important;
}

.matrix-title-area {
  justify-content: center;
  flex-direction: column;
}

.matrix-title {
  font-size: 14px;
}

.matrix-sub-title {
  font-size: 12px;
}

.matrix-length {
  font-size: 12px;
}

.matrix-content {
  font-size: 13px;
}
</style>