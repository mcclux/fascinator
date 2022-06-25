<template>
  <div>
    <Nuxt />
    <div>
      <NavBar
        :errorui="errorui"
        :display-error-bar="displayErrorBar"
        :dismiss-error-bar="dismissErrorBar"
        :wallet="wallet"
        :update-wallet="updateWallet"
        :networks="networks"
        :cnetwork="cnetwork"
        :update-network="updateNetwork"
      />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { BeaconWallet } from '@taquito/beacon-wallet'
Vue.prototype.$beaconwallet = new BeaconWallet({ name: 'fascinator' })
export default Vue.extend({
  data () {
    return {
      wallet: {
        address: '',
        balance: '',
        isConnected: false
      },
      errorui: {
        hasError: false,
        errorMessage: ''
      },
      networks: {
        mainnet: {
          networkname: 'Mainnet',
          nodes: ['https://mainnet.api.tez.ie', 'https://mainnet.smartpy.io', 'https://rpc.tzbeta.net/', 'https://teznode.letzbake.com', 'https://mainnet-tezos.giganode.io']
        },
        jakartanet: {
          networkname: 'Jakartanet',
          nodes: ['https://rpc.jakartanet.teztnets.xyz']
        },
        ithacanet: {
          networkname: 'Ithacanet',
          nodes: ['https://ithacanet.ecadinfra.com', 'https://ithacanet.smartpy.io/']
        }
      },
      cnetwork: {
        networkname: 'Mainnet',
        node: 'https://mainnet.api.tez.ie'
      }
    }
  },
  methods: {
    displayErrorBar (message:string) {
      this.errorui.hasError = true
      this.errorui.errorMessage = message
    },
    dismissErrorBar () {
      this.errorui.hasError = false
      this.errorui.errorMessage = ''
    },
    updateWallet (address:string, connected:boolean) {
      this.wallet.address = address
      this.wallet.isConnected = connected
    },
    updateNetwork (networkname:string, node:string) {
      this.cnetwork.networkname = networkname
      this.cnetwork.node = node
    }
  }
})
</script>
