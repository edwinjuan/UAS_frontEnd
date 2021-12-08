<template>
    <main>
        <v-app-bar color="amber" darken-2>
            <v-toolbar-title class="font-weight-black ml-10">Connect Us</v-toolbar-title>
           
            <v-spacer></v-spacer>

            <v-form class="mt-10 mb-2">
                <v-container>
                    <v-form v-model="valid" ref="formLogin">
                    <v-row>
                        <v-col cols="6" sm="4">
                            <v-text-field v-model="emailLog" :rules="emailRules" required solo outlined clearable class="mr-5" label="E-mail" type="text">
                            </v-text-field>
                        </v-col>
                        <v-col cols="6" sm="4">
                            <v-text-field v-model="passwordLog" :rules="passwordRules" required solo outlined  label="password" type="password">
                            </v-text-field>
                        </v-col>
                        <v-col cols="6" sm="4">
                            <v-btn color="blue" class="mt-2 d-flex align-center" darken @click="login">Login</v-btn>
                        </v-col>
                    </v-row>
                    </v-form>
                </v-container>
            </v-form>
        </v-app-bar>

        <v-container fluid fill-height class="posisinya">
            <v-layout flex align-center justify-center>
                    <v-flex x512 sm6 elevation-6>
                        <h3 style="text-align:center; font-weight:bold">Rating</h3>
                        <v-list-item
                            v-for="(feedback, i) in this.feedbacks"
                            :key="i"
                        >
                        <v-list-item-content>
                            <FeedbackCard
                                v-bind:id="feedback.id"
                                v-bind:username="feedback.name"
                                v-bind:feedback_star="feedback.feedback_star"
                                v-bind:feedback_content="feedback.feedback_content"
                            ></FeedbackCard>
                        </v-list-item-content>
                        </v-list-item>

                        <v-snackbar v-model="snackbar" :color="color" timeout="2000" bottom>{{ error_message }}</v-snackbar>
                    </v-flex>
                </v-layout>
            <v-layout flex align-center justify-center>
                    <v-flex x512 sm6 elevation-6>
                        <v-toolbar class="grey darken-3">
                            <v-toolbar-title class="grey--text">
                                <h1>Register</h1>
                            </v-toolbar-title>
                        </v-toolbar>
                        <v-card>
                            <v-card-text class="pt-4">
                                <div>
                                    <v-form v-model="valid" ref="form">
                                        <v-text-field v-model="name" :rules="nameRules" outlined required label="Name" type="text"></v-text-field>
                                        <v-select v-model="gender" :rules="genderRules" :items="genderList" label="Gender" outlined
                                        ></v-select>
                                        <v-text-field v-model="dateborn" :rules="datebornRules" outlined required label="Date Born" type="date"></v-text-field>
                                        <v-text-field v-model="email" :rules="emailRules" outlined required label="Email" type="email"></v-text-field>
                                        <v-text-field v-model="username" :rules="usernameRules" outlined required label="Username" type="text"></v-text-field>
                                        <v-text-field v-model="password" :rules="passwordRules" outlined required label="Password" type="password"></v-text-field>
                                        
                                        <v-layout justify-center>
                                            <v-btn color="blue" @click="register" :class="{ 'grey darken-1 white--text' : valid, disable: !valid }">Register</v-btn>
                                        </v-layout>
                                    </v-form>
                                </div>
                            </v-card-text>
                        </v-card>
                        <v-snackbar v-model="snackbar" :color="color" timeout="2000" bottom>{{ error_message }}</v-snackbar>
                    </v-flex>
                </v-layout>
        </v-container>
    </main>
</template>

<style>
    @import url("https://fonts.googleapis.com/css?family=Jolly%20Lodger");
    .grey--text{
        font-family: "Jolly Lodger";
    }

    .posisinya{
        position: absolute;
        top: 60px;
        left: 0;
        right: 0;
    }
</style>

<script>
//jangan lupa ubah
import FeedbackCard from "./Post/FeedbackCard";


export default {
    name: "Login",
    components: {FeedbackCard},
    data() {
        return {
            emailLog: '',
            passwordLog: '',
            feedbacks: new Array(),
            genderList: ['Pria', 'Wanita'],
            valid: false,
            name: '',
            gender: '',
            dateborn: '',
            username: '',
            password: '',
            color: '',
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
            emailRules: [
                (v) => !!v || 'Email tidak boleh kosong :,(',
            ],
            usernameRules: [
                (v) => !!v || 'Username tidak boleh kosong :,(',
            ],
            passwordRules: [
                (v) => !!v || 'Password tidak boleh kosong :,(',
            ],
        };
    },
    methods: {
        login() {
            if (this.$refs.formLogin.validate()) {
                // cek validasi data yang terkirim
                this.load = true;
                this.$http.post(this.$api + '/login', {
                    email: this.emailLog,
                    password: this.passwordLog
                }).then(response => {
                    // simpan data id user yang diinput
                    localStorage.setItem('id', response.data.user.id);
                    localStorage.setItem('token', response.data.access_token);
                    this.error_message = response.data.message;
                    this.color = "green";
                    this.snackbar = true;
                    this.load = false;
                    this.clear();
                    this.$router.push({
                      name: 'Homepage',
                    });
                }).catch(error => {
                    this.error_message = error.response.data.message;
                    this.color = "red";
                    this.snackbar = true;
                    this.load = false;
                })
            }
        },

        clear() {
            this.$refs.form.reset() //clear form login
        },

        readFeedback()
        {
            var url = this.$api + '/feedback/index';
            this.$http.get(url).then(response => {
                this.feedbacks = response.data.data;
            })
        },

        register() {
            if (this.$refs.form.validate()) {
                // cek validasi data yang terkirim
                this.load = true;
                this.$http.post(this.$api + '/register', {
                    name: this.name,
                    gender: this.gender,
                    dateborn: this.dateborn,
                    email: this.email,
                    username: this.username,
                    password: this.password
                }).then(response => {
                    // simpan data id user yang diinput
                    this.error_message = response.data.message;
                    this.color = "green";
                    this.snackbar = true;
                    this.load = false;
                    this.clear();
                    this.$router.push({
                        name: 'Login',
                    });
                }).catch(error => {
                    this.error_message = error.response.data.message;
                    this.color = "red";
                    this.snackbar = true;
                    localStorage.removeItem('token');
                    this.load = false;
                })
            }
        }
    },
    
    mounted() {
        this.readFeedback();
  },
};
</script>