<template>
  <div>
    <div class="post" v-for="item in posts" :key="item.id">
      <div>
        <strong>из {{item.curr1}}</strong> : <strong>в {{item.curr2}}</strong> 
      </div>
      <div>
        {{item.result}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    posts: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
  .post {
    padding: 15px;
    border: 5px solid teal;
    margin-top: 15px;
  }
</style>
