<template>
    <v-layout align-center justify-center mt-8 mb-4>
        <a v-for="link in links" :key=link.name :href="link.fields.url" target = "_blank" class="social-link mr-2">
            <v-icon color="#42B2C1">mdi-{{link.fields.fontAwesomeIcon}}</v-icon>
        </a>
    </v-layout>
</template>

<script>
import ContentfulAdapter from '../contentful.js'

export default {
    data:function(){
      return {
        links:[],
      }
    },
    methods:{
      setData(){
        var vm = this;
        vm.loading =  true;
        ContentfulAdapter.getSocialLinks()
          .then(function (entry) {
            vm.links  =  entry.items;
          })
      },
    },
    created :function(){
      this.setData();
    },
  }

</script>

<style>
.social-link {
    text-decoration: none;
}
</style>
