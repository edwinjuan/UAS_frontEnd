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
                            <v-btn color="blue" class="mt-2 d-flex align-center" rounded darken @click="profile"><v-icon>mdi-account-tie</v-icon></v-btn>
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
                <v-select v-model="gender" color="black" item-color="black" :rules="genderRules" :items="genderList" label="Gender" outlined
                ></v-select>
                <v-text-field v-model="dateborn" color="black" :rules="datebornRules" outlined required label="Date Born" type="date"></v-text-field>
                <v-text-field v-model="username" color="black" :rules="usernameRules" outlined required label="Username" type="text"></v-text-field>
                <v-text-field v-model="password" color="black" outlined label="Password" type="password"></v-text-field>
                                        
                <v-layout justify-center>
                    <v-btn color="blue" @click="update" :class="{ 'blue white--text' : valid, disable: !valid }">Update</v-btn>
                </v-layout>
            </v-form>

          </v-container>
        </v-list>
      </v-navigation-drawer>


      <v-container fluid fill-height class="posisinya">
            <v-layout flex align-center justify>
                <v-col>

                <v-card
                class="mx-auto"
                color="#26c6da"
                dark
                max-width="500"
                >
                <v-card-title>
                <v-icon
                    large
                    left
                >
                    mdi-twitter
                </v-icon>
                <span class="text-h6 font-weight-light">Twitter</span>
                </v-card-title>

                <v-card-text class="text-h5 font-weight-bold">
                "Turns1 out semicolon-less style is easier and safer in TS because most gotcha edge cases are type invalid as well."
                </v-card-text>

                <v-card-actions>
                <v-list-item class="grow">
                    <v-list-item-avatar color="grey darken-3">
                    <v-img
                        class="elevation-6"
                        alt=""
                        src="https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light"
                    ></v-img>
                    </v-list-item-avatar>

                    <v-list-item-content>
                    <v-list-item-title>Evan You</v-list-item-title>
                    </v-list-item-content>

                    <v-row
                    align="center"
                    justify="end"
                    >
                    <v-icon class="mr-1">
                        mdi-heart
                    </v-icon>
                    <span class="subheading mr-2">256</span>
                    <span class="mr-1">·</span>
                    <v-icon class="mr-1">
                        mdi-share-variant
                    </v-icon>
                    <span class="subheading">45</span>
                    </v-row>
                    
                    
                </v-list-item>
                </v-card-actions>
            </v-card>
                <v-card
                class="mx-auto"
                color="#26c6da"
                dark
                max-width="500"
                >
                <v-card-title>
                <v-icon
                    large
                    left
                >
                    mdi-twitter
                </v-icon>
                <span class="text-h6 font-weight-light">Twitter</span>
                </v-card-title>

                <v-card-text class="text-h5 font-weight-bold">
                "Turns2 out semicolon-less style is easier and safer in TS because most gotcha edge cases are type invalid as well."
                </v-card-text>

                <v-card-actions>
                <v-list-item class="grow">
                    <v-list-item-avatar color="grey darken-3">
                    <v-img
                        class="elevation-6"
                        alt=""
                        src="https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light"
                    ></v-img>
                    </v-list-item-avatar>

                    <v-list-item-content>
                    <v-list-item-title>Evan You</v-list-item-title>
                    </v-list-item-content>

                    <v-row
                    align="center"
                    justify="end"
                    >
                    <v-icon class="mr-1">
                        mdi-heart
                    </v-icon>
                    <span class="subheading mr-2">256</span>
                    <span class="mr-1">·</span>
                    <v-icon class="mr-1">
                        mdi-share-variant
                    </v-icon>
                    <span class="subheading">45</span>
                    </v-row>
                    
                    
                </v-list-item>
                </v-card-actions>
            </v-card>

                <v-card
                class="mx-auto mt-4"
                color="#26c6da"
                dark
                max-width="500"
                >
                <v-card-title>
                <v-icon
                    large
                    left
                >
                    mdi-twitter
                </v-icon>
                <span class="text-h6 font-weight-light">Twitter</span>
                </v-card-title>

                <v-card-text class="text-h5 font-weight-bold">
                "Turns out semicolon-less style is easier and safer in TS because most gotcha edge cases are type invalid as well."
                </v-card-text>

                <v-card-actions>
                <v-list-item class="grow">
                    <v-list-item-avatar color="grey darken-3">
                    <v-img
                        class="elevation-6"
                        alt=""
                        src="https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light"
                    ></v-img>
                    </v-list-item-avatar>

                    <v-list-item-content>
                    <v-list-item-title>Evan You</v-list-item-title>
                    </v-list-item-content>

                    <v-row
                    align="center"
                    justify="end"
                    >
                    <v-icon class="mr-1">
                        mdi-heart
                    </v-icon>
                    <span class="subheading mr-2">256</span>
                    <span class="mr-1">·</span>
                    <v-icon class="mr-1">
                        mdi-share-variant
                    </v-icon>
                    <span class="subheading">45</span>
                    </v-row>
                    
                    
                </v-list-item>
                </v-card-actions>
            </v-card>

            

                </v-col>
            </v-layout>
      </v-container>

    
    <v-snackbar v-model="snackbar" :color="color" timeout="2000" bottom>{{ error_message }} </v-snackbar>
    </main>
</template>

<script>
export default {
    name: "Profile",
    data() {
        return {
            load: false,
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
            usernameRules: [
                (v) => !!v || 'Username tidak boleh kosong :,(',
            ],
            passwordRules: [
                (v) => !!v || 'Password tidak boleh kosong :,(',
            ],
        };
    },
    methods: {
        readProfile() {
            this.idUser = localStorage.getItem('id');

            var url = this.$api + '/users/' + this.idUser;
            this.$http.get(url, {
                headers: {
                    'Authorization' : 'Bearer ' + localStorage.getItem('token')
                }
            }).then(response => {
                this.name = response.data.data['name'];
                this.gender = response.data.data['gender'];
                this.dateborn = response.data.data['dateborn'];
                this.username = response.data.data['username'];
                this.password = response.data.data['password'];
            })
            
        },
        homepage() {
            this.$router.push({
                name: 'Homepage',
            });
        },
        update(){
            let newData= {
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
                    'Authorization' : 'Bearer ' + localStorage.getItem('token')
                }
            }).then(response =>{
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
    
    mounted(){
        this.readProfile();
    },
};
</script>