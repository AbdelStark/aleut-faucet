<template>
  <v-container>
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
            cols="4"
        >
          <v-text-field
              flat solo placeholder="Type your Ethereum address"
              hide-details="auto"
              v-model="recipient"
          ></v-text-field>
        </v-col>
      </v-row>

      <v-col
          class="mb-2"
          cols="12"
      >
        <v-btn color="indigo accent-4"

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
export default {
  name: 'Faucet',

  data: () => ({
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

    },
  }
}
</script>
