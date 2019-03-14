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
div {
  left:0;
  right:0;
  top:0;
  bottom: 0;
  position: fixed;
  background-color: rgb(202, 202, 202);
}
</style>
