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
                    <h2 class="font-weight-black black--text">ConnectUs</h2>
                </div>
            </v-list-item-content>
          </v-list-item>

          <v-divider class="black"></v-divider>

            <v-list-item>
                <v-list-item-title class="black--text"> FOLLOWERS </v-list-item-title>
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

    

    </main>
</template>

<style>
    .posisinya{
        position: absolute;
        top: 60px;
        left: 0;
        right: 0;
    }
</style>

<script>
export default {
    name: "Login",
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
            idPar: ''
        };
    },
    methods: {
        readFollower() {
            this.idUser = localStorage.getItem('id');

            var url = this.$api + '/followers/name/' + this.idUser;
            this.$http.get(url, {
                headers: {
                    'Authorization' : 'Bearer ' + localStorage.getItem('token')
                }
            }).then(response => {
                this.namaFollowers = response.data.data;
            })
            
        },
        profile() {
            this.$router.push({
                name: 'Profile',
            });
        },
        followerName(idPar){
            var url = this.$api + '/users/' + idPar;
            this.$http.get(url, {
                headers: {
                    'Authorization' : 'Bearer ' + localStorage.getItem('token')
                }
            }).then(response => {
                return response.data.data['name'];
            })
        },
        
    },
    
    mounted(){
        this.readFollower();
    },
};
</script>