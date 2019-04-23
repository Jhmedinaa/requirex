<template>
  <tabs tabs @on-click="handleTabs">
    <tabPane :label="$t('requirex_application')" name="application" v-if="tab0">      
      <h1>{{ $t("requirex_application_tittle")}}</h1>      
      <router-view></router-view>
    </tabPane>

    <tabPane :label="$t('requirex_domain')" name="domain" v-if="tab0">
      <h1>{{ $t("requirex_domain_tittle") }}</h1>
      <router-view></router-view>
    </tabPane>

    <tabPane :label="$t('requirex_adaptation')" name="adaptation" v-if="tab0">
      <h1>{{ $t("requirex_adaptation_tittle")}}</h1>
      <router-view></router-view>
    </tabPane>
  </tabs>
</template>

<script src="//unpkg.com/vue/dist/vue.js"></script>
<script src="//unpkg.com/iview/dist/iview.min.js"></script>
<script>
export default {
  data() {
    return {
      tab0: true,
      tab1: true,
      tab2: true
    };
  },
  methods: {
    handleTabs(name) {
      this.$router.push("/requirex/" + name);
    }
  }
};
</script>