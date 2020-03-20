<template>
  <v-app-bar app elevation="2" color="white">
    <v-toolbar flat>
      <v-img
        class="mx-2"
        src="../assets/logo.svg"
        max-height="40"
        max-width="40"
        contain
      ></v-img>
      <v-toolbar-title>
        Intugine
      </v-toolbar-title>
      <v-spacer />
      <v-toolbar-items>
        <v-btn exact to="/" text>Home</v-btn>
        <v-btn exact to="#" text>Brands</v-btn>
        <v-btn exact to="#" text>Transporters</v-btn>
      </v-toolbar-items>
      <v-btn class="mx-2" elevation="0" fab small color="rgb(190,193,201)">
        <img src="../assets/profile.svg" width="20px" />
      </v-btn>
      <v-menu v-model="showMenu" offset-y style="max-width: 600px">
        <template v-slot:activator="{ on }">
          <v-icon v-on="on">mdi-chevron-down</v-icon>
        </template>
        <v-list>
          <v-list-item v-for="(item, index) in items" :key="index">
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-toolbar>
  </v-app-bar>
</template>

<script>
export default {
  data() {
    return {
      showMenu: false,
      items: [
        { title: "Click Me" },
        { title: "Click Me" },
        { title: "Click Me" },
        { title: "Click Me 2" }
      ]
    };
  }
};
</script>

<style>
.v-btn{
    text-transform: none !important;
}
</style>
