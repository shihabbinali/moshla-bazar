<template>
    <div id="nested-links" class="row">
        <span> 
            <a v-on:click="clickAllCategory()">
                <span>All Categories</span>
                <span v-if="currentContextLength">&nbsp;{{ '>' }}&nbsp;</span>
            </a> 
        </span>
        <span v-for="(root, index) in $store.getters.currentContext.immediateroots" :key="index"> 
            <a v-on:click="click(root.nodeid)">
                <span>{{root.name}}</span>
                <span v-if="index < $store.getters.currentContext.immediateroots.length-1">&nbsp;{{ '>' }}&nbsp;</span>
            </a> 
        </span>
    </div>
</template>

<script>
export default {
  methods: {
      clickAllCategory: function() {
            this.$store.dispatch('closeAllMenue');
            this.$store.dispatch('setCurrentContext', {
                context: {},
                router: this.$router
            });            
      },
      click: function(nodeid) {            
            this.$store.dispatch('setExpandFlagTrueAndSelectAndCloseOthers', nodeid);
            this.$store.dispatch('setCurrentContext', {
                context: nodeid,
                router: this.$router
            });
      }
  },
  computed: {
      currentContextLength () {
          const length = Object.keys(this.$store.getters.currentContext).length;          
          return (length > 0);
      }
  }  
}
</script>


<style scoped>
#nested-links {
    padding: 10px;
}
span {
    font-weight: 600;
    cursor: pointer;
    color: grey;
}

span :active {
    color: black;
}
</style>
