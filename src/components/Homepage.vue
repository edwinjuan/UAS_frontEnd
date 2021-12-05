<template>
  <main>

    <v-app-bar color="amber" darken- style="height: 80px">

      <v-spacer></v-spacer>

      <v-form class="mt-10 mb-4">
        <v-container>
          <v-row>
            <v-col cols="6" sm="6">
              <v-text-field v-model="search" required solo rounded label="Search" type="text">
              </v-text-field>
            </v-col>
            <v-col cols="6" sm="3">
              <v-btn color="grey" class="mt-2 d-flex align-center" rounded darken @click="cari">Cari!</v-btn>
            </v-col>
            <v-col cols="6" sm="1">
              <v-btn color="blue" class="mt-2 d-flex align-center" rounded darken @click="profile">
                <v-icon>mdi-account-tie</v-icon>
              </v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-form>
    </v-app-bar>

    <v-navigation-drawer
        v-model="drawer"
        color="amber lighten-2"
        absolute
        dark
    >
      <v-list dense nav
              class="py-0"
      >
        <v-list-item>
          <v-list-item-content>
            <div class="d-flex justify-center">
              <h2 class="font-weight-black black--text">ConnectUs</h2>
            </div>
          </v-list-item-content>
        </v-list-item>

        <v-divider class="black"></v-divider>

        <v-list-item>
          <v-list-item-title class="black--text"> FOLLOWERS</v-list-item-title>
        </v-list-item>


        <v-list-item
            v-for="(follower, i) in this.namaFollowers"
            :key="i"
            link
        >
          <v-list-item-icon>
            <v-icon class="black">mdi-account-multiple-outline</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title class="black--text">{{ follower }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-list-item
        v-for="(post, i) in this.posts"
        :key="i"
    >
      <v-list-item-content>
        <PostCard
            v-bind:username="post.name"
            v-bind:post-content="post.post_content"
            v-bind:comments="post.comments"
        ></PostCard>
      </v-list-item-content>
    </v-list-item>
  </main>
</template>

<style>
.posisinya {
  position: absolute;
  top: 60px;
  left: 0;
  right: 0;
}
</style>

<script>
import PostCard from "./Post/PostCard";

export default {
  name: "Login",
  components: {PostCard},
  data() {
    return {
      load: false,
      snackbar: false,
      error_message: '',
      color: '',
      valid: false,
      name: '',
      namaFollowers: [],
      idUser: '',
      idPar: '',
      posts:[],
      comments: [],
      // posts: [
      //   {
      //     id: 1,
      //     post_content: "Hello ini contoh post pertama " +
      //         "banyak hal yang harus dikerjakan " +
      //         "bersama Tuhan kita pasti bisa. " +
      //         "Amiinn.",
      //     user_id: 1,
      //     comments: [
      //       {
      //         user_id: "Thomas Shelby",
      //         content: "good post!"
      //       },
      //       {
      //         user_id: "Jane Doe",
      //         content: "great!"
      //       },
      //       {
      //         user_id: "Thomas Shelby",
      //         content: "good post!"
      //       },
      //       {
      //         user_id: "Jane Doe",
      //         content: "great!"
      //       },
      //       {
      //         user_id: "Thomas Shelby",
      //         content: "good post!"
      //       },
      //       {
      //         user_id: "Jane Doe",
      //         content: "great!"
      //       },
      //     ],
      //   },
      //   {
      //     id: 2,
      //     post_content: "Hello ini contoh post kedua",
      //     user_id: 2,
      //     comments: [],
      //   },
      //   {
      //     id: 3,
      //     post_content: "Hello ini contoh post ketiga",
      //     user_id: 2,
      //     comments: [
      //       {
      //         user_id: "Thomas Shelby",
      //         content: "good post!"
      //       },
      //       {
      //         user_id: "Jane Doe",
      //         content: "great!"
      //       },
      //     ],
      //   },
      //   {
      //     id: 4,
      //     post_content: "Hello ini contoh post pertama",
      //     user_id: 4,
      //     comments: [
      //       {
      //         user_id: "Thomas Shelby",
      //         content: "good post!"
      //       },
      //       {
      //         user_id: "Jane Doe",
      //         content: "great!"
      //       },
      //     ],
      //   },
      //   {
      //     id: 5,
      //     post_content: "Hello ini contoh post kedua",
      //     user_id: 2,
      //     comments: [],
      //   },
      //   {
      //     id: 6,
      //     post_content: "Hello ini contoh post ketiga",
      //     user_id: 3,
      //     comments: [
      //       {
      //         user_id: "Thomas Shelby",
      //         content: "good post!"
      //       },
      //       {
      //         user_id: "Jane Doe",
      //         content: "great!"
      //       },
      //     ],
      //   },
      // ],

    };
  },
  methods: {
    readFollower() {
      this.idUser = localStorage.getItem('id');

      var url = this.$api + '/followers/name/' + this.idUser;
      this.$http.get(url, {
        headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response => {
        this.namaFollowers = response.data.data;
      })

    },
    readPosts() {
      var url = this.$api + '/post/'
      this.$http.get(url, {
        headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response => {
        this.posts = response.data.data;
      })
    },
    profile() {
      this.$router.push({
        name: 'Profile',
      });
    },
    followerName(idPar) {
      var url = this.$api + '/users/' + idPar;
      this.$http.get(url, {
        headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response => {
        return response.data.data['name'];
      })
    },

  },

  mounted() {
    this.readFollower();
    this.readPosts();
  },
};
</script>