<template>
<div>
  <div>父组件</div>
  <child :message="parentMsg"></child>
</div>


</template>

<script>
  import child from './child'
  export default {
    name: 'parnet',
    components:{
        child
    },
    data () {
      return {
        parentMsg: 'Welcome to Your Vue.js App'
      }
    }
  }
</script>

