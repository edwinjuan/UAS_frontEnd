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
    </v-card-title>

    <v-card-text class="text-h5 font-weight-bold"> {{ postContent }}</v-card-text>
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
                mdi-heart
              </v-icon>
            </v-col>
            <v-col>
              <v-icon class="mr-1">
                mdi-share-variant
              </v-icon>
            </v-col>
          </v-row>
          <template v-slot:actions>
            <v-icon>
              mdi-comment
            </v-icon>
          </template>
        </v-expansion-panel-header>

        <v-expansion-panel-content
            color="#5098fb"
        >
          <v-form>
            <v-text-field
                type="text"
                placeholder="new comment..."
                hint="type a new comment to this post"
            ></v-text-field>
            <v-btn align="end"
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
                v-bind:username="comment.user_id"
                v-bind:comment="comment.content"
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
  props: ['username', 'postContent', 'comments'],
  name: "PostCard"
}
</script>

<style scoped>
.scrollbar-hide::-webkit-scrollbar {
  display: none;
}
</style>