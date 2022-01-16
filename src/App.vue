<template>
  <div id="root" :class="getColorTheme" class="antialiased pt-18">
    <div id="header" :class="getIsScrolled ? 'shadow-xl' : ''" class="flex flex-1 fixed inset-x-0 top-0 st5 bg-gradient-to-r dark:from-avalabDark-gray dark:to-slightDark from-gray-300 to-slightGray z-50">
      <Header />
    </div>

    <div id="body" class="flex w-full avalab-layout z-20 st5 bg-gradient-to-r from-gray-300 to-slightGray dark:from-avalabDark-gray dark:to-slightDark">
      <router-view />
    </div>

    <div id="footer" class="w-full h-full z-40 st5 bg-gradient-to-r from-gray-300 to-slightGray dark:from-avalabDark-gray dark:to-slightDark">
      <Footer />
    </div>
  </div>
</template>

<script>
  import Header from '@/components/Header';
  import Footer from '@/components/Footer';
  import { mapActions, mapGetters } from 'vuex';
  import avalab from "@/shared/avalab.js";


  export default {
    name: 'AVALab',
    mixins: [avalab],
    components: {
      Header,
      Footer,
    },
    created() {
      window.addEventListener('scroll', this.handleScroll);
    },
    mounted: async function() {
      
      // Color Mode!
      let theme = localStorage.getItem("AVALab\_theme");

      if (theme) {
        this.setTheme(theme);
      } else {
        localStorage.setItem("AVALab\_theme", 'dark');
      }

    },

    computed: {
      ...mapGetters('user', ['getIsScrolled', 'getColorTheme']),
    },
    
    methods: {
      ...mapActions('user', ['setIsScrolled', 'setTheme']),
      ...mapActions('wallet', ['switchWalletType']),


      handleScroll() {
        this.setIsScrolled(window.scrollY > 0)
      }
    },
  };
</script>