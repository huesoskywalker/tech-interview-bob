<template>
  <v-container>
    <v-row>
      <v-card style="width: 100%">
        <v-card-title class="searchBar">
          <v-text-field
            v-model.trim="searchText"
            dense
            filled
            rounded
            clearable
            placeholder="Search"
            prepend-inner-icon="mdi-magnify"
            class="pt-6 shrink expanding-search"
            :class="{ closed: searchBoxClosed && !searchText }"
            @focus="searchBoxClosed = false"
            @blur="searchBoxClosed = true"
          ></v-text-field>
        </v-card-title>
        <v-data-table
          v-if="!error"
          style="width: 100%; height: max-content"
          class="itemKey"
          :headers="headers"
          :items="bloodTypes"
          :search="searchText"
          :loading="isLoading"
        >
        </v-data-table>
        <v-alert v-if="error" :value="true" type="error">
          {{ error }}
        </v-alert>
      </v-card>
    </v-row>
    <v-row> </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    headers: [
      { text: "Type", align: "center", value: "type" },
      { text: "Rh Factor", align: "center", value: "rh_factor" },
      { text: "Group", align: "center", value: "group" },
    ],
    searchText: "",
    searchBoxClosed: true,
    bloodTypes: [],
    isLoading: true,
    error: null,
  }),

  created() {
    this.loadData();
  },

  methods: {
    async loadData() {
      try {
        const res = await fetch(
          `https://random-data-api.com/api/v2/blood_types?size=30`,
          {
            headers: {
              Accept: "application/json",
            },
            method: "GET",
          }
        );
        if (!res.ok) {
          throw new Error(`Something went wrong. Please try again.`);
        }
        /**
         * @type {BloodType[]}
         */
        const data = await res.json();

        this.bloodTypes = data;
        this.isLoading = false;
      } catch (error) {
        this.error = error.message;
        this.isLoading = false;
      }
    },
  },
};
/**
 * @typedef {Object} BloodType
 * @property {number} id
 * @property {string} uid
 * @property {string} type
 * @property {string} rh_factor
 * @property {string} group
 */
</script>

<style>
.searchBar {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
