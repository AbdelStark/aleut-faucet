<template>
  <v-app>
    <v-app-bar
      app
      color="indigo accent-4"
      dark
    >
      <div class="d-flex align-center">
        Aleut Faucet
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="http://eip1559-testnet.ops.pegasys.tech:3000/"
        target="_blank"
        text
      >
        <span class="mr-2">Explorer</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
      <v-btn
          href="http://eip1559-testnet.ops.pegasys.tech:3001/"
          target="_blank"
          text
      >
        <span class="mr-2">Network</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Faucet/>
    </v-main>
  </v-app>
</template>

<script>
import Faucet from './components/Faucet';

export default {
  name: 'App',

  components: {
    Faucet,
  },

  data: () => ({
    //
  }),
};
</script>
