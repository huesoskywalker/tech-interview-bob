<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-bottom-navigation
        style="
          background-color: transparent;
          width: fit-content;
          box-shadow: none;
        "
      >
        <ul>
          <li v-for="link in navLinks">
            <v-btn :to="link.to">
              {{ link.text }}
              <v-icon>{{ link.icon }} </v-icon>
            </v-btn>
          </li>
        </ul>
      </v-bottom-navigation>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    navLinks: [
      { to: "/", text: "Home", icon: "mdi-home" },
      { to: "/about", text: "About", icon: "mdi-information-variant" },
      { to: "/data", text: "Data", icon: "mdi-magnify" },
    ],
  }),
};
</script>

<style>
ul {
  list-style-type: none;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}
</style>
