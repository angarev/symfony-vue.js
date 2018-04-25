<template>
    <ul v-if="posts && posts.length">
        <li v-for="post of posts">
            <p><strong>{{post.name}}</strong></p>
            <p>{{post.email}}</p>
        </li>
    </ul>

    <ul v-else="errors && errors.length">
        <li v-for="error of errors">
            {{error.message}}
        </li>
    </ul>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        posts: [],
        errors: []
      }
    },
    created: function () {
      this.loadPush();
    },
    methods: {
      loadPush: function () {
        axios.get(`http://jsonplaceholder.typicode.com/users`).then(response => {
          // JSON responses are automatically parsed.
          this.posts = response.data
        }).catch(e => {
          this.errors.push(e)
        })
      }
    }
  }
</script>