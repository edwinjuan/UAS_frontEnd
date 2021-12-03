<template>
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
        <v-list-item-title>{{ username }}}</v-list-item-title>
      </v-list-item-content>
      <v-card-text class="text-h5 font-weight-bold"> {{ comment }}</v-card-text>
    </v-list-item>
  </v-card-actions>
</template>

<script>
export default {
  props: ['username','comment'],
  name: "Comment"
}
</script>

<style scoped>

</style>