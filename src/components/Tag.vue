<template>
    <div class="tag">
        <router-link class = "tag-link" :to="`/tag/${tag.fields.enName}`">
            #{{tag.fields.jaName}}<span v-if="showCount">({{count}})</span>
        </router-link>
    </div>
</template>

<script>
import ContentfulAdapter from '../contentful.js'

export default {
    props: ['tag','showCount'],
    data:function(){
    return {
        count:null,
    }
  },
    methods:{
      setData(){
          var vm =  this;
        ContentfulAdapter.getBlogCountByTagId(this.tag.sys.id)
        .then(function (entry) {
            vm.count = entry.total;
          })
      },
    },
    created :function(){
        this.setData();
    }
}

</script>


<style scoped>
.tag {
    margin-right: 8px;
}

.tag-link{
  color:#7f8d8e!important;
  text-decoration: none;
}

.tag-link:hover {
  color: #42B2C1!important;
  text-decoration: underline;
}

</style>

