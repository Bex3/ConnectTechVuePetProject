<template>
  <div>
    <v-list aria-owns="roles">
      <v-subheader v-if="!favorites.length" aria-label="your favorites are empty">Your favorites list is empty</v-subheader>
      <div v-else>
        <v-subheader>My Favorite Doggos</v-subheader>
        <v-list-item v-for="(dog, index) in favorites" :key="index" @click="{}">
          <v-list-item-avatar>
            <img :src="dog.img">
          </v-list-item-avatar>
          <v-list-item-content>{{dog.name}}</v-list-item-content>
          <v-list-item-action>
            <v-icon @click="removeFromFavorites(dog)">delete</v-icon>
          </v-list-item-action>
        </v-list-item>
        <v-btn to="/form">Adopt</v-btn>
      </div>
    </v-list>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  computed: {
    favorites() {
      return this.$store.state.favorites;
    }
  },
  methods: {
    ...mapActions(["removeFromFavorites"])
  }
};
</script>
