<template>
  <v-app>
      <codeEditor></codeEditor>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import codeEditor from './components/codeEditor.vue';

export default Vue.extend({
  name: 'App',

  components: {
    codeEditor,
  },

  data: () => ({
    //
  }),
});
</script>
