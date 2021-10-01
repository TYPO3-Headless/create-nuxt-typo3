<%_ if (skin) { _%>
<template>
  <UiLayout>
    <template #header>
      <CwHeader />
    </template>
    <CwBreadcrumbs v-if="showBreadcrumbs" />
    <nuxt />
    <template #footer>
      <CwFooter />
    </template>
  </UiLayout>
</template>
<script lang="ts">
import Vue from 'vue'
import { mapGetters } from 'vuex'
import UiLayout from 'nuxt-typo3-theme/src/components/UiLayout/UiLayout.vue'
import CwHeader from 'nuxt-typo3-theme/src/components/CwHeader/CwHeader.vue'
import CwFooter from 'nuxt-typo3-theme/src/components/CwFooter/CwFooter.vue'
import CwBreadcrumbs from 'nuxt-typo3-theme/src/components/CwBreadcrumbs/CwBreadcrumbs.vue'
export default Vue.extend({
  components: {
    UiLayout,
    CwHeader,
    CwFooter,
    CwBreadcrumbs
  },
  head () {
    return {
      htmlAttrs: {
        lang: this.$typo3.i18n.locale
      }
    }
  },
  computed: {
    ...mapGetters(['breadcrumbs']),
    showBreadcrumbs () {
      return this.breadcrumbs.length > 1
    }
  }
})
</script>
<%_ } else { _%>
<template>
  <div>
    <div class="links">
      <nuxt-link :to="navMain.link">
        {{ navMain.title }}
      </nuxt-link>
      <template v-if="navMain.children">
        <nuxt-link
          v-for="(item, key) in navMain.children"
          :key="key"
          :to="item.link"
        >
          {{ item.title }}
        </nuxt-link>
      </template>
    </div>
    <div class="links">
      <lang-switcher />
    </div>
    <nuxt />
  </div>
</template>
<script>
import { mapState } from 'vuex'
export default {
  computed: {
    ...mapState({
      navMain: state => state.typo3.initial.navigation[0] || [] // get first instance from root
    })
  }
}
</script>
<style>
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.button--green {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #3b8070;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #fff;
  background-color: #3b8070;
}

.button--grey {
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #35495e;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--grey:hover {
  color: #fff;
  background-color: #35495e;
}
.links {
  text-align: center;
}

.links a {
  text-decoration: none;
  margin: 0 15px;
}
</style>
<%_ } _%>
