<template>
  <div class="form">
    <h3>Add a Post</h3>
    <label for="body">Body: </label>
    <input name="body" type="text" id="body" required v-model="post.body" />
    <div class="buttons">
      <button @click="addPost" class="center">Add Post</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddPost",
  data() {
    return {
      post: {
        date: "",
        body: "",
      },
    };
  },
  methods: {
    addPost() {
      var data = {
        date: new Date().toLocaleDateString(),
        body: this.post.body,
      };
      fetch("http://localhost:3000/api/posts", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      })
      .then((response) => {
        console.log(response.data);
        this.$router.push("/api/allposts");
      })
      .catch((e) => {
        console.log(e);
        console.log("error");
      });
    },
  },
};
</script>

<style scoped>
.form {
  max-width: 420px;
  margin: 30px auto;
  background: #5A6267;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
h3 {
  text-align: center;
  color: lightgray;
}
label {
  color: lightgray;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.8em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid white;
  color: black;
}
button {
  margin: 0 auto;
  text-align: center;
  color: black;
  border: 0;
  padding: 10px 20px;
  border-radius: 20px;
}

button:hover {
  transform: scale(1.05) perspective(1px);
}

.buttons{
  margin: 0 auto;
  text-align: center;
}

.center{
  background-color: gray;
  border: 0;
  margin-top:  20px;
  margin-right:  10px;
  border-radius: 25px;
}
</style>