<template>
    <v-app>
      <CostCenter/>
    </v-app>
</template>

<script>
import CostCenter from './components/CostCenter';

export default {
  name: 'App',

  components: {
    CostCenter,
  },

  data: () => ({
    //
  }),
};
</script>
