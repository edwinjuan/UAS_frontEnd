<template>
  <v-card-actions>
    <v-list-item class="grow">
      <v-col>
        <v-row>
          <v-list-item-avatar color="grey darken-3">
            <v-img
                class="elevation-6"
                alt=""
                src="https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light"
            ></v-img>
          </v-list-item-avatar>
          <v-list-item-content>
            <v-list-item-title class="fw-bold">{{ username }}</v-list-item-title>
          </v-list-item-content>
        </v-row>
        <v-row class="">
          <v-card-text>{{ comment }}</v-card-text>
        </v-row>
      </v-col>
    </v-list-item>
  </v-card-actions>
</template>

<script>
export default {
  props: ['username', 'comment'],
  name: "Comment"
}
</script>

<style scoped>

</style>