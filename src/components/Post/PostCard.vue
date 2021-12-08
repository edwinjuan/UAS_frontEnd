<template>
  <v-card
      class="mx-auto"
      color="#26c6da"
      dark
      max-width="700"
  >
    <v-card-title>
      <v-icon
          large
          left
      >
        mdi-account-circle
      </v-icon>
      <span class="text-h6 font-weight-light">{{ username }}</span>
      <v-spacer></v-spacer>
      <div>
          <v-icon @click="updatePost" class="mr-2" v-if="status==='edit'">mdi-pencil</v-icon>
          <v-icon @click="deletePost" v-if="status==='edit'">mdi-delete</v-icon>
      </div>
    </v-card-title>

    <v-card-text v-if="status==='show'" class="text-h5 font-weight-bold"> {{ postContent }}</v-card-text>

    <div v-else style="background-color:red; display:flex; flex:row" justify="center" class="text-xs-center">
        <v-text-field v-model="postContent" :disabled="disable" class="mx-5 text-h5 font-weight-bold shrink"></v-text-field>
        <v-btn style="align-item:center" @click="updateApi" :hidden="hiden">Edit</v-btn>
    </div>
    <!--    comment section using expand panels -->
    <v-expansion-panels>
      <v-expansion-panel
          style="max-height: 50vh; overflow: scroll; scroll-behavior: smooth;"
          class="scrollbar-hide">
        <v-expansion-panel-header style="position: sticky; top: 0; z-index: 2" color="#26c6da" disable-icon-rotate>
          <v-row
              class="mx-4 my-n4"
              align="center"
              justify="end"
          >
            <v-col>
              <v-icon class="mr-1">
                
              </v-icon>
            </v-col>
            <v-col>
              <v-icon class="mr-1">
                mdi-comment
              </v-icon>
            </v-col>
          </v-row>
          <template v-slot:actions>
            <v-icon>
              
            </v-icon>
          </template>
        </v-expansion-panel-header>

        <v-expansion-panel-content
            color="#5098fb"
        >
          <v-form>
            <v-text-field
                v-model="newComment"
                type="text"
                placeholder="new comment..."
                hint="type a new comment to this post"
            ></v-text-field>
            <v-btn @click="createComment" align="end"
                   color="#26c6da"
                   type="submit"
            >
              post
              <v-icon
              >mdi-near-me
              </v-icon>
            </v-btn>
          </v-form>
          <div
              v-for="(comment, i) in this.comments"
              :key="i">
            <Comment
                v-bind:username="comment.name"
                v-bind:comment="comment.content"
                v-bind:idComment="comment.id"
                v-bind:idUser="comment.user_id"
            ></Comment>
          </div>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>


  </v-card>

</template>

<script>
import Comment from "./Comment";

export default {
  components: {Comment},
  props: ['id', 'username', 'postContent', 'comments', 'status'],
  name: "PostCard",
  data() {
      return {
        newComment: '',
        disable: true,
        hiden: true,
      };
  },
  methods: {
      createComment() {
          let idusercok = localStorage.getItem('id');
          let newData= {
                content : this.newComment,
            };
          var url = this.$api + '/comment/' + this.id + '/' + idusercok;
          
          this.$http.post(url, newData, {
            headers: {
              'Authorization': 'Bearer ' + localStorage.getItem('token')
            }
          }).then(response => {
            console.log(response.data.message);
            
        }).catch(error => {
                alert(error.response.data.message);
        });
         alert("Comment Added");
      },
      deletePostApi() {
          var url = this.$api + '/post/' + this.id;
          
          this.$http.delete(url,{
            headers: {
              'Authorization': 'Bearer ' + localStorage.getItem('token')
            }
          }).then(response => {
            console.log(response.data.message);
          }).catch(error => {
                  alert(error.response.data.message);
          });
      },
      deleteCommentPost() {
          var url = this.$api + '/comment/post/' + this.id;
          
          this.$http.delete(url,{
            headers: {
              'Authorization': 'Bearer ' + localStorage.getItem('token')
            }
          }).then(response => {
            console.log(response.data.message);
          });
      },
      deletePost() {
         this.deleteCommentPost();
         this.deletePostApi();
         alert("Post berhasil dihapus");
         window.location.reload();
      },
      updatePost() {
        this.hiden = false;
        this.disable =  false;
      },
      updateApi() {
          let newData= {
              post_content : this.postContent,
          };
          var url = this.$api + '/post/' + this.id;
          
          this.$http.put(url, newData, {
            headers: {
              'Authorization': 'Bearer ' + localStorage.getItem('token')
            }
          }).then(response => {
            console.log(response.data.message);
            this.hiden = true;
            this.disable =  true;
            alert("Post Edited");
            window.location.reload();
        }).catch(error => {
                alert(error.response.data.message);
        });
      },
  },
};


</script>

<style scoped>
.scrollbar-hide::-webkit-scrollbar {
  display: none;
}
</style>