<template>
<div class="wrapper">
  <div class="posts">
    <div class="post" v-for="post in posts" :key="post.id">
      <div class="info" :style="'background-color:' + post.color">
          <div class="username">
            <h1>{{post.userName}}</h1>
          </div>
        <div class="button">
          <div v-if="onMyPage()">
            <div v-if="notFollowing(post.userName)">
              <button class="auto"><a v-on:click="follow(post)">Follow {{post.userName}}</a></button>
            </div>
            <div v-else>
              <button class="auto"><a v-on:click="unFollow(post)">UnFollow {{post.userName}}</a></button>
            </div>
          </div>
          <div v-else>
            <button class="auto"><a v-on:click="deletePost(post)">Delete Post</a></button>
          </div>
        </div>
      </div>
      <div class="middle">
        <div class="middle-item">
          <div class="image">
            <img :src="'/images/'+post.image">
          </div>
        </div>
        <div class="middle-item">
            <div class="description">
              <p> {{post.description}} </p>
            </div>
          </div>
        </div>
        <div class="description" :style="'background-color:' + post.color">
          <div class="bottom">
            <div class="bottom-item">
              <div class="tag">
                <div v-for="value in post.tags" :key="value.id">
                  <div class="tag-item">
                  <h2> #{{value}} </h2>
                  </div>
                </div>
            </div>
          </div>
          <img :src="'/images/'+post.heart" style="width: 50px; margin-right: 30px;" v-on:click="liked(post)">
          </div>
          <div class="bottom-item">
          <p>Posted in - {{post.country}}</p>
        </div>
        </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'PostList',
  props: {
    posts: Array
  },
  methods: {
    follow(post) {
      var userName = post.userName;
      if(!this.$root.$data.following.includes(userName)) {
        this.$root.$data.following.push(userName);
      }
    },
    notFollowing(userName) {
      if(this.$root.$data.following.includes(userName)) {
        return false;
      }
      else {
        return true;
      }
    },
    unFollow(post) {
      var userName = post.userName;
      var index = -1;
      for(var i = 0; i < this.$root.$data.following.length; i++) {
        if(this.$root.$data.following[i] == userName) {
          index = i;
        }
      }
      this.$root.$data.following.splice(index, 1);
    },
    onMyPage() {
      if(this.$root.$data.bold == 2) {
        return false;
      }
      else {
        return true;
      }
    },
    deletePost(post) {
      for(var i = 0; i < this.$root.$data.posts.length; i++) {
        if(post.id == this.$root.$data.posts[i].id) {
          this.$root.$data.posts.splice(i, 1);
          console.log(this.$root.$data.posts);
        }
      }
    },
    liked(post) {
      if(post.heart == "noColorHeart.png") {
        post.heart = "colorHeart.png"
      }
      else {
        post.heart = "noColorHeart.png"
      }
    },
  }
}
</script>

<style scoped>
.bottom {
  display: flex;
  align-items: left;
  text-align: left;
  width: 100%;
}

.bottom-item {
  width: 100%;
  display: flex;
}

.tag {
  display: flex;
  align-items: left;
  justify-content: flex-start;
  text-align: left;
}

.tag-item {
  margin-right: 10px;
  display: flex;
}

.delete {
  background-color: red;
}

.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}

.tags {
  display: inline;
}

.posts {
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.middle {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.middle-item {
  width: 700px;
  margin-left: 5%;
  margin-right: 5%;
  display: flex;
}

.post {
  border: 2px solid black;
  margin: 10px;
  margin-top: 50px;
  margin-right: 30px;
  margin-left: 30px;
  width: 50%;
  background-color: white;
}

.post img {
  margin-top: 5px;
  border: 2px solid #333;
  height: 90%;
  width: 90%;
  object-fit: cover;
}

.post .image {
  display: flex;
  justify-content: center;
  margin-bottom: 5px;
}

.info {
  display: flex;
  background: #daebe8;
  color: #000;
  padding: 10px 30px;
  height: 80px;
}

.username {
  font-size: 25px;
  width: 80%;
}

.button {
  width: 100px;
  text-align: right;
}

.description {
  text-align: left;
  padding-left: 10px;
  padding-bottom: 8px;
}

.info h1 {
  font-size: 100%;
  text-align: left;
}

.info h2 {
  font-size: 14px;
}

h2 {
  font-size: 20px;
}

.info p {
  text-align: left;
  font-size: 90%;
}

button {
  height: 50px;
  background: #000;
  color: white;
  border: none;
}

.auto {
  margin-left: auto;
}

</style>
