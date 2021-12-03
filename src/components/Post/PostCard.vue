<template>
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
        mdi-post
      </v-icon>
      <span class="text-h6 font-weight-light">{{ username }}</span>
    </v-card-title>

    <v-card-text class="text-h5 font-weight-bold"> {{ postContent }}</v-card-text>
    <v-row
        class="m-4"
        align="center"
        justify="end"
    >
      <v-col>
        <v-icon class="mr-1">
          mdi-heart
        </v-icon>
      </v-col>
      <v-col>
        <span class="subheading mr-2">256</span>
      </v-col>
      <v-col>
        <v-icon class="mr-1">mdi-comment</v-icon>
      </v-col>

      <v-col>
        <span class="subheading">45</span>
      </v-col>
      <v-col>
        <v-icon class="mr-1">
          mdi-share-variant
        </v-icon>
      </v-col>
    </v-row>
<!--    comment   -->
    <v-list-item
        v-for="(comment, i) in this.comments"
        :key="i"
        link
    >
      <v-list-item-content>
        <Comment
        v-bind:username="comment.user_id"
        v-bind:comment="comment.content"
        ></Comment>
      </v-list-item-content>
    </v-list-item>
  </v-card>

</template>

<script>
import Comment from "./Comment";
export default {
  components: {Comment},
  props: ['username','postContent','comments'],
  name: "PostCard"
}
</script>

<style scoped>

</style>