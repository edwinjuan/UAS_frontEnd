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
              <v-btn color="grey" class="mt-2 d-flex align-center" rounded darken @click="logout">Logout</v-btn>
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

        <v-list-item>
          <v-list-item-avatar>
            <v-img src="https://randomuser.me/api/portraits/men/85.jpg"></v-img>
          </v-list-item-avatar>

          <v-list-item-title class="black--text">John Leider</v-list-item-title>
        </v-list-item>
        <v-list-item>
          <v-list-item-avatar>
            <v-img src="https://randomuser.me/api/portraits/men/85.jpg"></v-img>
          </v-list-item-avatar>

          <v-list-item-title class="black--text">John Leider</v-list-item-title>
        </v-list-item>
        <v-list-item>
          <v-list-item-avatar>
            <v-img src="https://randomuser.me/api/portraits/men/85.jpg"></v-img>
          </v-list-item-avatar>

          <v-list-item-title class="black--text">John Leider</v-list-item-title>
        </v-list-item>
        <v-list-item>
          <v-list-item-avatar>
            <v-img src="https://randomuser.me/api/portraits/men/85.jpg"></v-img>
          </v-list-item-avatar>

          <v-list-item-title class="black--text">John Leider</v-list-item-title>
        </v-list-item>

        
      </v-list>
    </v-navigation-drawer>

    <v-list-item
        v-for="(post, i) in this.posts"
        :key="i"
    >
      <v-list-item-content>
        <PostCard
            v-bind:id="post.id"
            v-bind:username="post.name"
            v-bind:post-content="post.post_content"
            v-bind:comments="bindComment(post.id)"
            v-bind:status="status"
        ></PostCard>
      </v-list-item-content>
    </v-list-item>

    <v-snackbar v-model="snackbar" color="blue" timeout="2000" bottom>Masuk sini</v-snackbar>
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
      valid: false,
      name: '',
      namaFollowers: [],
      idUser: '',
      idPar: '',
      status: 'show',
      posts:new Array(),
      comments: [],
      post: [],
      comment: '',
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
    readComments() {
      var url = this.$api + '/comment/'
      this.$http.get(url, {
        headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response => {
        this.comments = response.data.data;
        
      })
    },
    readPosts() {
      var url = this.$api + '/post'
      this.$http.get(url, {
        headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response => {
        // this.posts = response.data.data;
        this.posts = response.data.data;
      })
    },
    bindComment(id) {
      let hasil = new Array();
        for (let i=0; i<this.comments.length; i++) {
            if (id === this.comments[i].post_id) {
              hasil.push(this.comments[i]);
            }
        }
        return hasil;
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

    logout() {
			localStorage.removeItem('id');
      localStorage.removeItem('token');
      location.reload();
		},

  },

  created() {
    this.readFollower();
    this.readPosts();
    this.readComments();
  },
};
</script>