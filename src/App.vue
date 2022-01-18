
<template lang="">
  <div class="app">
     <post-form 
     @create="createPost" />
     <post-list 
      :posts="posts" />
      

  </div>
</template>
<script>
import PostForm from './components/PostForm.vue'
import PostList from './components/PostList.vue'
export default {
  components: {
    PostForm, PostList
  },
  data() {
    return {
      posts:[
        // {
        //   val1: 1,
        //   val2: 'JS',
        //   result: 'Язык программирования'
        // },
        // {
        //   val1: 2,
        //   val2: 'Python',
        //   result: 'Язык программирования'
        // },
        // {
        //   val1: 3,
        //   val2: 'C#',
        //   result: 'Язык программирования'
        // },
      ]
    }
  },
  methods: {
    // addLike(){
    //   this.likes += 1
    // },
    // addDislike(){
    //   this.dislike += 1
    // }
    createPost(post){
      this.posts.unshift(post)
    }
  },
}
</script>
<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  .app {
    padding: 20px;
  }

  
</style>
