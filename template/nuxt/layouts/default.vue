<%_ if (skin) { _%>
<template>
  <div class="wrapper">
    <header-main>
      <template v-slot:before>
        <language-switcher
          :active="currentLanguage"
          :languages="availableLanguages"
          class="container flex justify-end"
        />
      </template>
      <template v-slot:logo>
        <nuxt-link :to="navMain.link" class="flex h-full items-center">
          <logo />
        </nuxt-link>
      </template>
      <template v-slot:navigation>
        <navigation-main :links="navMain.children" />
      </template>
    </header-main>
    <div class="section-main">
      <div v-if="breadcrumbs" class="border-b mb-20px">
        <breadcrumbs :links="breadcrumbs" class="container" />
      </div>
      <nuxt />
    </div>
    <footer-main>
      <template v-slot:credits>
        <nuxt-link :to="navMain.link" class="flex h-full items-center">
          <logo />
        </nuxt-link>
      </template>
    </footer-main>
  </div>
</template>
<script>
import {
  NavigationMain,
  Logo,
  HeaderMain,
  FooterMain,
  Breadcrumbs,
  LanguageSwitcher
} from 'nuxt-typo3-skin/components'
import { mapState } from 'vuex'
export default {
  components: {
    NavigationMain,
    HeaderMain,
    FooterMain,
    Logo,
    Breadcrumbs,
    LanguageSwitcher
  },
  computed: {
    ...mapState({
      navMain: state => state.typo3.initial.navigation[0] || [], // get first instance from root tree,
      breadcrumbs: state => state.typo3.page.page.breadcrumbs || [], // get breadcrumbs for current page,
      currentLanguage: state => state.typo3.locale,
      availableLanguages: state => state.typo3.page.languages
    })
  }
}
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
