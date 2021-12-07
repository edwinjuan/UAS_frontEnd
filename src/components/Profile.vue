<template>
  <main>

    <v-app-bar color="amber" darken-2>

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
              <h2 class="font-weight-black black--text" @click="homepage">ConnectUs</h2>
            </div>
          </v-list-item-content>
        </v-list-item>

        <v-divider class="black"></v-divider>

        <v-list-item>
          <div class="d-flex justify-center">
            <h5 class="black--text">Data Profile</h5>
          </div>
        </v-list-item>

        <v-container class="amber darken-3" fluid>

          <v-form v-model="valid" ref="form">
            <v-text-field v-model="name" :rules="nameRules" outlined required label="Name" type="text"></v-text-field>
            <v-select v-model="gender" color="black" item-color="black" :rules="genderRules" :items="genderList"
                      label="Gender" outlined
            ></v-select>
            <v-text-field v-model="dateborn" color="black" :rules="datebornRules" outlined required label="Date Born"
                          type="date"></v-text-field>
            <v-text-field v-model="username" color="black" :rules="usernameRules" outlined required label="Username"
                          type="text"></v-text-field>
            <v-text-field v-model="password" color="black" outlined label="Password" type="password"></v-text-field>

            <v-layout justify-center>
              <v-btn color="blue" @click="update" :class="{ 'blue white--text' : valid, disable: !valid }">Update
              </v-btn>
            </v-layout>
          </v-form>

        </v-container>

        <v-list-item>
                <div class="d-flex justify-center">
                    <h5 class="black--text">Feedback</h5>
                </div>
            </v-list-item>
              

          <v-container class="amber darken-3" fluid>
              
            <v-form v-model="valid" ref="form">
                <v-text-field v-model="review" :rules="reviewRules" outlined required label="Review" type="text"></v-text-field>
                <v-select v-model="star" color="black" item-color="black" :rules="starRules" :items="starList" label="Star" outlined
                ></v-select>
                                        
                <v-layout justify-center>
                    <div v-if="review != ''">
                      <v-btn color="blue" @click="updateFeedback" :class="{ 'blue white--text' : valid, disable: !valid }">Update</v-btn>
                      <v-btn color="red" @click="deketeFeedback" :class="{ 'red white--text' : valid, disable: !valid }">Delete</v-btn>
                    </div>
                    <div v-else>
                      <v-btn color="green" @click="createFeedback" :class="{ 'green white--text' : valid, disable: !valid }">Create</v-btn>
                    </div>
                </v-layout>
            </v-form>

          </v-container>


      </v-list>
    </v-navigation-drawer>

    <CreatePost
        class="mt-15"
        v-bind:username="username"
        v-bind:user_id="user_id"
    ></CreatePost>

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
        ></PostCard>
      </v-list-item-content>
    </v-list-item>

    <v-snackbar v-model="snackbar" :color="color" timeout="2000" bottom>{{ error_message }}</v-snackbar>
  </main>
</template>

<script>
import CreatePost from "./Post/CreatePost";
import PostCard from "./Post/PostCard";

export default {

  name: "Profile",
  components: {PostCard, CreatePost},
  data() {
    return {
      load: false,
      posts: new Array(),
      genderList: ['Pria', 'Wanita'],
      valid: false,
      user_id: localStorage.getItem('id'),
      name: '',
      gender: '',
      dateborn: '',
      username: '',
      password: '',
      color: '',
      review: '',
      star: '',
      comments: [],
      snackbar: false,
      error_message: '',
      nameRules: [
        (v) => !!v || 'Name tidak boleh kosong :,(',
      ],
      genderRules: [
        (v) => !!v || 'Gender tidak boleh kosong :,(',
      ],
      datebornRules: [
        (v) => !!v || 'Dateborn tidak boleh kosong :,(',
      ],
      usernameRules: [
        (v) => !!v || 'Username tidak boleh kosong :,(',
      ],
      passwordRules: [
        (v) => !!v || 'Password tidak boleh kosong :,(',
      ],
      reviewRules: [
        (v) => !!v || 'Review tidak boleh kosong :,(',
      ],
      starRules: [
        (v) => !!v || 'Star tidak boleh kosong :,(',
      ],
      starList: ['1', '2', '3', '4', '5'],
    };
  },
  methods: {
    readProfile() {
      this.idUser = localStorage.getItem('id');

      var url = this.$api + '/users/' + this.idUser;
      this.$http.get(url, {
        headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response => {
        this.name = response.data.data['name'];
        this.gender = response.data.data['gender'];
        this.dateborn = response.data.data['dateborn'];
        this.username = response.data.data['username'];
        this.password = response.data.data['password'];
      })

    },
    readPosts() {
      var url = this.$api + '/postfrom/' + this.idUser
      this.$http.get(url, {
        headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response => {
        this.posts = response.data.data;
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
    bindComment(id) {
      let hasil = new Array();
      for (let i=0; i<this.comments.length; i++) {
        if (id === this.comments[i].post_id) {
          hasil.push(this.comments[i]);
        }
      }
      return hasil;
    },
    homepage() {
      this.$router.push({
        name: 'Homepage',
      });
    },
    readFeedback() {
      this.idUser = localStorage.getItem('id');

      var url = this.$api + '/feedback/' + this.idUser;
      this.$http.get(url, {
      headers: {
        'Authorization' : 'Bearer ' + localStorage.getItem('token')
      }
      }).then(response => {
        this.review = response.data.data['feedback_content'];
        this.star = response.data.data['feedback_star'];
      })
    },

    updateFeedback(){
      let newData= {
      feedback_content: this.review,
        feedback_star: this.star
        }

      var url = this.$api + '/feedback/' + this.idUser;
      this.load = true;
      this.$http.put(url, newData, {
        headers: {
          'Authorization' : 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response =>{
        this.error_message = response.data.message;
        this.color = "green";
        this.snackbar = true;
        this.load = false;
        this.close();
        this.readFeedback();
      }).catch(error => {
        this.error_message = error.response.data.message;
        this.color = "red";
        this.snackbar = true;
        this.load = false;
      });
    },

    deleteFeedback(){
      this.idUser = localStorage.getItem('id');

      var url = this.$api + '/feedback/' + this.idUser;
      this.$http.delete(url, {
      headers: {
        'Authorization' : 'Bearer ' + localStorage.getItem('token')
      }
      });
    },

    update() {
      let newData = {
        name: this.name,
        gender: this.gender,
        dateborn: this.dateborn,
        email: this.email,
        username: this.username,
        password: this.password
      }

      var url = this.$api + '/users/' + this.idUser;
      this.load = true;
      this.$http.put(url, newData, {
        headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response => {
        this.error_message = response.data.message;
        this.color = "green";
        this.snackbar = true;
        this.load = false;
        this.close();
        this.readProfile(); // baca data
      }).catch(error => {
        this.error_message = error.response.data.message;
        this.color = "red";
        this.snackbar = true;
        this.load = false;
      });
    },

  },

  mounted() {
    this.readProfile();
    this.readFeedback();
    this.readPosts();
    this.readComments();
  },
};
</script>