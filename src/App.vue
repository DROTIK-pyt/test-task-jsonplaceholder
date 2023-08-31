<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-sm-4 offset-sm-4 col-12">
          <form @submit.prevent="emptyEvent" action="">
            <div class="form-group">
              <input
                type="text"
                autocomplete="off"
                @change="search"
                v-model="userNameSearch"
                class="form-control"
                placeholder="Filter by author.."
              />
            </div>
          </form>
        </div>
      </div>
      <div class="row">
        <div
          v-show="!isEmptySearch"
          v-for="post in posts"
          :key="post.id"
          class="col-sm-4 col-12"
        >
          <CardPost
            :title="post.title"
            :body="post.body"
            :userName="authorName(post.userId)"
          />
        </div>
        <div class="col-12" v-show="isEmptySearch">Posts not found.</div>
      </div>
    </div>
  </div>
</template>

<script>
import CardPost from "./components/CardPost.vue";

export default {
  name: "Test-task",
  data: function () {
    return {
      posts: [],
      users: [],
      allPosts: [],
      userNameSearch: "",
      isEmptySearch: false,
    };
  },
  components: {
    CardPost,
  },
  methods: {
    authorName(userId) {
      return (
        this.users.find((user) => userId == user.id)?.name ||
        "Author not found."
      );
    },
    search() {
      let usersFound = [];
      if (this.userNameSearch.length > 1) {
        this.users.forEach((user) => {
          if (user.name == this.userNameSearch) {
            usersFound.push(user.id);
          }
        });
        this.posts = this.posts.filter((post) =>
          usersFound.includes(post.userId)
        );
      } else {
        this.posts = this.allPosts;
      }
      this.isEmptySearch = this.posts.length == 0;
    },
    emptyEvent() {},
  },
  beforeMount() {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((users) => {
        this.users = users;
      });
    fetch("https://jsonplaceholder.typicode.com/posts")
      .then((res) => res.json())
      .then((posts) => {
        this.posts = posts;
        this.allPosts = posts;
      });
  },
};
</script>
