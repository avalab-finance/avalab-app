<template>
  <div v-if="isOpen" class="flex ml-2 justify-between">
    <div class="flex min-w-0 w-full h-12 space-x-3">
      <!-- Earned Info -->
      <div class="flex w-20 flex-col h-full justify-between">
        <div class="flex space-x-2 items-center">
          <i class="las la-hand-holding-usd text-avalabGreen"></i>
          <p class="text-xs font-extralight text-avalabBlue-light">Earned</p>
        </div>
        <p class="text-sm font-bold dark:text-gray-300 text-el">{{pendingReward}}</p>
      </div>
      <!-- Liquidity Info -->

    </div>
    <!-- Open Details Button -->
    <div class="flex h-12 items-end">
      <div @click="setPool()" class="flex h-9 items-center space-x-2 rounded-full group bg-gray-100 hover:bg-gray-200 dark:bg-avalabDark-gray dark:hover:bg-gray-900 pl-3 cursor-pointer">
        <p class="text-sm text-gray-500 dark:text-avalabBlue-light">details</p>
        <i class="las la-arrow-down text-lg p-2 text-gray-500 dark:text-avalabBlue-light rounded-full bg-gray-100 dark:bg-avalabDark-gray group-hover:bg-avalabGreen dark:group-hover:text-avalabDark-gray group-hover:text-gray-100 border-2 border-gray-200 dark:border-gray-700"></i>
      </div>
    </div>
  </div>
</template>

<script>
  import avalab from "@/shared/avalab.js";
  import { ethers } from "ethers";
  export default {
    name: 'PoolStatsClosed',
    mixins: [avalab],
    props: {
      isOpen: Boolean,
      pool: Object,
      poolData: Object
    },
    data() {
      return {
        liquidityValue: '',
        pendingReward: '',
      }
    },
    mounted: async function (){
      setInterval(
        function(){
          this.pendingReward = this.getEthUnits(this.poolData.pendingReward)
        }.bind(this), 1000
      )
      

    },
    methods: {
      setPool() {
        this.$emit('setPool', 'open');
        if (window.innerWidth >= 768) {
          this.avalabEmit.emit("recalc-tooltips");
        }
      }
    }
  }
</script>