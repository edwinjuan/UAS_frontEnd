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
        mdi-post
      </v-icon>
      <span class="text-h6 font-weight-light"> Hello {{ username }}, with id: {{ user_id }}  Tell ur friends what you feel today :)</span>
    </v-card-title>
    <v-card-text>
      <v-textarea
          background-color="teal"
          v-model="inputPost"
      />

      <div style="display: flex; justify-content: center">
      <v-btn @click="createPost"
             color="teal"
             type="submit"
      >
        post
        <v-icon
        >mdi-near-me
        </v-icon>

      </v-btn>
      </div>
    </v-card-text>
    <!--    <v-card-text class="text-h5 font-weight-bold"> {{ postContent }}</v-card-text>-->

  </v-card>
</template>

<script>
export default {
  name: "CreatePost",
  props: ['username','user_id'],
  data() {
    return {
      inputPost: '',
    }
  },
  methods: {
    createPost(){
      var url = this.$api + '/post' ;
      let newData={
        post_content: this.inputPost,
        user_id: this.user_id
      }
      this.$http.post(url, newData, {
        headers: {
          'Authorization': 'Bearer ' + localStorage.getItem('token')
        }
      }).then(response => {
        alert(response.data.message);
      })
    },
  }
}
</script>

<style scoped>

</style>