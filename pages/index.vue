<template>
  <div class="main">
    <v-container style="max-width: 1000px; position: relative; margin-bottom: 100px;">
      <v-row>
        <v-col>
          <v-row no-gutters>
            <v-col align="center" justify="center"><v-img :src="require(`~/assets/logo.svg`)"
                max-width="200"></v-img></v-col>
          </v-row>
          <v-row>
            <p>The acronym SCTM refers to the Smart Contract TTP Matrix. It provides an analytical framework to
              understand and anticipate the Tactics, Techniques, and Procedures (TTPs) deployed by attackers against Smart
              Contracts, a promising and emerging technology within the blockchain space. By understanding the SCTM,
              developers of Smart Contracts can gain insight into which tactics and techniques need to be prioritized and
              safeguarded against. For those wishing to delve deeper into this, please click on the <NuxtLink to="/why">
                'Why?'</NuxtLink> tab.</p>
            <p>This matrix is inspired by and developed from the <a href="https://attack.mitre.org/" target="_blank"
                rel="noopener noreferrer">MITRE ATT&CK
                framework</a> and the <a href="https://swcregistry.io/" target="_blank" rel="noopener noreferrer">SWC
                Registry</a>, which catalog
              known vulnerabilities. It consolidates possible TTPs that can occur in Smart Contracts, offering a
              comprehensive overview of potential threat landscapes in the realm of blockchain-based contracts.</p>
          </v-row>
        </v-col>
        <v-col align="center" justify="center" style="align-self: center;"><v-img
            :src="require(`~/assets/korea_university.png`)" max-width="200"></v-img>
        </v-col>
      </v-row>
    </v-container>
    <v-row no-gutters class="matrix-item" style="margin-bottom: 100px;">
      <v-col v-for="(item, index) in items" :key="index" lg="1.5">
        <v-card class="elevation-0">
          <v-card-title class="matrix-title-area">
            <div class="matrix-title" @click="() => $router.push({
              name: 'tactics-tactic',
              params: {
                tactic: item.to.replace('/', ''),
              }
            })">{{ item.title }}</div>
            <div class="matrix-sub-title">{{ item.subTitle ?? "&nbsp;" }}</div>
            <div class="matrix-length">{{ item.items.length }} techniques</div>
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
  head: {
    title: `HOME`,
  },
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
  cursor: pointer;
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

a {
  text-decoration: none;
}</style>