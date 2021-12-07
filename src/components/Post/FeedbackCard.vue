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
      <span class="text-h6 font-weight-light">{{ username }} - {{ feedback_star }}</span>
    </v-card-title>

    <v-card-text class="text-h5 font-weight-bold"> {{ feedback_content }}</v-card-text>
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
      </v-expansion-panel>
    </v-expansion-panels>


  </v-card>

</template>
<style scoped>
.scrollbar-hide::-webkit-scrollbar {
  display: none;
}
</style>