<template>
  <v-app>
    <v-app-bar fixed app dark class="elevation-0" color="#7f0025">
      <v-toolbar-title style="cursor: pointer" @click="$router.push('/')">{{ title }}</v-toolbar-title>
      <v-spacer />
      <div v-for="(item, index) in menu" :key="index">
        <v-menu v-if="item.items && item.items.length > 0" offset-y>
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="#fff" plain dark v-bind="attrs" v-on="on">
              {{ item.title }}
            </v-btn>
          </template>
          <v-list>
            <v-list-item v-for="(item, index) in item.items" :key="index">
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
        <v-btn v-else color="#fff" plain dark :to="item.to">
          {{ item.title }}
        </v-btn>
      </div>
    </v-app-bar>
    <v-main>
      <Nuxt />
    </v-main>
    <v-footer app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      title: 'Smart Contract TTP Matrix | SCTM',
      menu: [
        {
          title: 'Tactics',
          to: '/tactics',
        },
        {
          title: 'Techniques',
          to: '/techniques',
        },
        {
          title: 'Why?',
          to: '/why',
        },
        {
          title: 'Profile',
          to: '/profile',
        }
      ],
    }
  }
}
</script>
<style lang="scss">
.page-enter-active,
.page-leave-active {
  transition: opacity 0.5s;
}
.page-enter,
.page-leave-to {
  opacity: 0;
}
</style>