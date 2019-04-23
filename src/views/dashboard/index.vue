<template>
  <div class="dashboard-container">
    <div class="dashboard-text">name:{{ name }}</div>
    <div class="dashboard-text">roles:<span v-for="role in roles" :key="role">{{ role }}</span></div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
// import adminDashboard from './admin'
// import editorDashboard from './editor'

export default {
  name: 'Dashboard',
  // components: { adminDashboard, editorDashboard },
  // data() {
  //   return {
  //     currentRole: 'adminDashboard'
  //   }
  // },
  // computed: {
  //   ...mapGetters([
  //     'roles'
  //   ])
  // },
  computed: {
    ...mapGetters([
      'name',
      'roles'
    ])
  }
  // created() {
  //   if (!this.roles.includes('admin')) {
  //     this.currentRole = 'editorDashboard'
  //   }
  // }
}
</script>
