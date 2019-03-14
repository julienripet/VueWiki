<template>
  <div>
    <app-header/>
    <app-main />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
  props:[],
  components:{
    'app-header':Header,
    'app-main':Main
  },
  data () {
    return {
      
    }
  },
  methods:{
    
  }
}

</script>

<style scoped>

</style>
