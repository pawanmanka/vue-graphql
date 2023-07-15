<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    {{books}}
    
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },
  data(){
    return{
      books:[]
    }
  },
  created(){
    this.getBooks();
  },
  methods:{
    async getBooks(){
      let res = await axios.post('http://127.0.0.1:8000/graphql', {
                query: `{
                  books {
                    id
                    title
                    author
                  }
                }`
              });
      this.books = res.data.data.books;
    }
  }

}
</script>
