<template>
  <!-- Add disabled -->
  <transition tag="div" name="approve-btn" class="inline-block absolute">
    <div v-if="this.getBtnState({add: 'disabled'})" class="flex w-28 st5 st5-all justify-between items-center border dark:border-gray-600 border-gray-300 space-x-1 p-2 pl-3 rounded-full group dark:bg-gray-700 bg-gray-200 select-none">
      <div class="flex flex-1 items-center justify-center">
        <p class="text-sm text-gray-300 dark:text-gray-600">Add</p>
      </div>
      <i class="las la-times-circle text-xl text-gray-300 dark:text-gray-600"></i>
    </div>
  </transition>

  <!-- Ready to Add -->
  <transition tag="div" name="approve-btn" class="inline-block absolute">
    <div @click="executeAddLiquidity()" v-if="this.getBtnState({add: 'add'})" class="flex w-28 group">
      <div class="grab-attention-glowing"></div>
      <div class="grab-attention cursor-pointer st5">
        <div class="flex flex-1 items-center justify-center">
          <p class="text-sm text-avalabGreen-dark dark:text-avalabGreen group-hover:text-gray-50 dark:group-hover:text-avalabDark-gray">Add</p>
        </div>
        <i class="las la-plus text-xl text-avalabGreen-dark dark:text-avalabGreen group-hover:text-gray-50 dark:group-hover:text-avalabDark-gray"></i>
      </div>
    </div>
  </transition>

  <!-- Adding -->
  <transition tag="div" name="approve-btn" class="inline-block absolute">
    <div v-if="this.getBtnState({add: 'adding'})" class="flex w-28 st5 group">
      <div class="grab-attention-glowing"></div>
      <div class="grab-attention cursor-wait st5">
        <div class="flex flex-1 items-center justify-center">
          <p class="text-sm text-avalabGreen-dark dark:text-avalabGreen group-hover:text-gray-50 dark:group-hover:text-avalabDark-gray">Adding</p>
        </div>
        <i class="las la-sync text-xl animate-spin text-avalabGreen-dark dark:text-avalabGreen group-hover:text-gray-50 dark:group-hover:text-avalabDark-gray"></i>
      </div>
    </div>
  </transition>

  <!-- Added -->
  <transition tag="div" name="approve-btn" class="inline-block absolute">
    <div v-if="this.getBtnState({add: 'added'})" class="flex w-28 st5 justify-between items-center border border-avalabGreen glow-avalabGreen-light-md space-x-1 p-2 pl-3 rounded-full dark:bg-avalabDark-gray bg-gray-100 cursor-default">
      <div class="flex flex-1 items-center justify-center">
        <p class="text-sm text-avalabGreen">Added</p>
      </div>
      <i class="las la-check-circle text-xl text-avalabGreen"></i>
    </div> 
  </transition>
</template>

<script>

  import { mapGetters, mapActions } from 'vuex'

  export default {
    name: 'LiquidityAddButton',
    props: {
      amount: String,
    },
    mounted: async function() {},
    
    computed: {
      ...mapGetters('liquidity/buttons', ['getBtnState']),
    },
    
    methods: {
      ...mapGetters('exchange', ['getToken']),      
      ...mapActions('liquidity/buttons', ['setBtnState']),

      executeAddLiquidity: async function() {
        this.$emit('executeAddLiquidity')
      }
    }
  }
</script>