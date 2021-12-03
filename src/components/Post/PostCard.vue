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
        mdi-twitter
      </v-icon>
      <span class="text-h6 font-weight-light">{{ username }}</span>
    </v-card-title>

    <v-card-text class="text-h5 font-weight-bold"> {{ postContent }}</v-card-text>

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