<template>
  <div>
    <div class="absolute top-0 px-3 pt-1 right-4">
      <button
        v-if="!wallet.isConnected"
        class="text-white"
        title="Connect Wallet"
        @click="connectwallet()"
      >
        <i class="fa-solid fa-wallet fa-xl mr-4 mt-4" />
      </button>
      <button
        v-if="wallet.isConnected"
        class="text-green-500"
        :title="wallet.address"
        @click="showDisconnectDiv = !showDisconnectDiv"
      >
        <i class="fa-solid fa-wallet fa-xl mr-4 mt-4" />
      </button>
      <div
        v-if="showDisconnectDiv"
        class="absolute rounded-md top-12 px-2 py-4 bg-gray-800 text-white text-xs right-0"
        @click="disconnectAndClose()"
      >
        <button>
          Disconnect
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    connectwallet: {
      type: Function,
      required: true
    },
    disconnectWallet: {
      type: Function,
      required: true
    },
    wallet: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      showDisconnectDiv: false
    }
  },
  methods: {
    disconnectAndClose () {
      this.disconnectWallet()
      this.showDisconnectDiv = false
    }
  }
})
</script>
