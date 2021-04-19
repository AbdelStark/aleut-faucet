<template>
  <v-container>
    <v-alert type="success" v-if="showSuccess" dismissible>
      Faucet request completed with success.
    </v-alert>
    <v-alert type="error" v-if="showFailed" dismissible>
      Faucet request failed.
    </v-alert>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
            :src="require('../assets/logo.svg')"
            class="my-3"
            contain
            height="200"
        />
      </v-col>

      <v-col class="mb-4" cols="12">
        <h1 class="display-2 font-weight-bold mb-3">
          Welcome to Aleut Faucet
        </h1>
      </v-col>
      <v-row justify="center">
        <v-col
            class="mb-2"
            cols="6"
        >
          <v-text-field
              flat solo placeholder="Your address"
              hide-details="auto"
              v-model="recipient"
          ></v-text-field>
        </v-col>
      </v-row>

      <v-col
          class="mb-2"
          cols="12"
      >
        <v-btn color="indigo accent-4" @click="requestFaucet"
               :loading="faucetLoading"
        >Request 5 ETH
        </v-btn>
      </v-col>
      <v-col
          class="mb-5"
          cols="12"
      >
        <h2 class="headline font-weight-bold mb-3">
          Important Links
        </h2>

        <v-row justify="center">
          <a
              v-for="(link, i) in importantLinks"
              :key="i"
              :href="link.href"
              class="subheading mx-3"
              target="_blank"
          >
            {{ link.text }}
          </a>
        </v-row>
      </v-col>

    </v-row>
  </v-container>
</template>

<script>
const axios = require('axios').default;
const rpcUrl = 'http://13.54.148.154:8545';

export default {
  name: 'Faucet',

  data: () => ({
    faucetLoading: false,
    showSuccess: false,
    showFailed: false,
    recipient: null,
    importantLinks: [
      {
        text: 'EIP-1559 Resources',
        href: 'https://hackmd.io/@timbeiko/1559-updates/https%3A%2F%2Fhackmd.io%2F%40timbeiko%2F1559-resources',
      },
    ],
  }),
  methods: {
    requestFaucet() {
      this.showFailed = false
      this.showSuccess = false
      this.faucetLoading = true
      console.log('requesting faucet for address: ', this.recipient)
      const payload = buildRequest(this.recipient);
      console.log(payload);
      axios.post(rpcUrl, payload)
          .then(this.faucetRequestSuccess)
          .catch(this.faucetRequestError);
    },
    faucetRequestSuccess(response) {
      this.faucetLoading = false
      console.log(response)
      // eslint-disable-next-line no-prototype-builtins
      const error = response.data.hasOwnProperty("error");
      console.log(error)
      if (error) {
        this.showFailed = true
      } else {
        this.showSuccess = true
      }
    },
    faucetRequestError(error) {
      console.error(error)
      this.faucetLoading = false
      this.showFailed = true
    }
  }
}

function buildRequest(address) {
  return {
    "method": "debug_faucet",
    "id": 1,
    "jsonrpc": "2.0",
    "params": [
      address,
    ]
  }
}
</script>
