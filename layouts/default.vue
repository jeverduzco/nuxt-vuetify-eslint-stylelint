<script setup lang="ts">
// import the useTheme composable
import { useTheme, useDisplay } from "vuetify";
const theme = useTheme();
const { name } = useDisplay();
// change the theme function
const changeTheme = () => {
  theme.global.name.value = theme.global.current.value.dark ? "light" : "dark";
};
// navigation drawer props
const navBarProps = reactive({
  expand: false,
  expandOnHover: true,
  rail: false
});
// create navigation drawer toggle function
const toggleNavBar = () => {
  if (name.value === "xs" || name.value === "sm" || name.value === "md") {
    navBarProps.expandOnHover = false;
    navBarProps.rail = false;
    navBarProps.expand = !navBarProps.expand;
  } else {
    navBarProps.expandOnHover = true;
    navBarProps.rail = !navBarProps.rail;
  }
};
</script>
<template>
  <div>
    <v-card>
      <v-app>
        <v-navigation-drawer
          v-model="navBarProps.expand"
          :expand-on-hover="navBarProps.expandOnHover"
          :rail="navBarProps.rail"
        >
          <v-list>
            <v-list-item
              prepend-avatar="https://randomuser.me/api/portraits/women/85.jpg"
              title="Sandra Adams"
              subtitle="sandra_a88@example.com"
            />
          </v-list>

          <v-divider />

          <v-list density="compact" nav>
            <v-list-item prepend-icon="mdi-folder" title="My Files" value="myfiles" />
            <v-list-item prepend-icon="mdi-account-multiple" title="Shared with me" value="shared" />
            <v-list-item prepend-icon="mdi-star" title="Starred" value="starred" />
          </v-list>
        </v-navigation-drawer>

        <v-app-bar>
          <template #prepend>
            <v-app-bar-nav-icon @click.stop="toggleNavBar" />
          </template>
          <v-app-bar-title>Nuxt 3 + Vuetify</v-app-bar-title>
          <template #append>
            <v-btn icon="mdi-theme-light-dark" @click="changeTheme" />
          </template>
        </v-app-bar>

        <v-main>
          <div class="pa-4">
            <slot />
          </div>
        </v-main>
      </v-app>
    </v-card>
  </div>
</template>
