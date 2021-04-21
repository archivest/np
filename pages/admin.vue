<template>
  <v-container>
    <h1>Admin</h1>
    <hr />
    You may delete categories and subcategories below, and upload images.
    Uploading an image to an inexistant category or subcategory (name them in
    the fields provided) will create them automatically. Deleting a category
    deletes all the subcategories therein. Deleting a subcategory deletes all
    the images therein.
    <hr />
    <h2>Categories</h2>
    <div>
      <v-list rounded>
        <v-list-item v-for="menuCategory in categories" :key="menuCategory">
          Category: <em>{{ menuCategory }}</em>
          <button @click="DeleteCategory(menuCategory)">Delete</button>
          <v-list rounded>
            <v-list-item
              v-for="menuSubCategory in Object.keys(staticData[menuCategory])"
              :key="menuSubCategory"
            >
              <v-list-item-title>
                Subcategory: <em>{{ menuSubCategory }}</em>
              </v-list-item-title>
              <button @click="DeleteSubcategory(menuCategory, menuSubCategory)">
                Delete
              </button>
            </v-list-item>
          </v-list>
        </v-list-item>
      </v-list>
    </div>
    <hr />
    <h2>Upload</h2>
    <form action="API_ENDPOINT" method="POST">
      <input id="cat" v-model="cat" type="text" placeholder="Category" />
      <input
        id="subcat"
        v-model="subcat"
        type="text"
        placeholder="Subcategory"
      />
      <input type="file" id="myFile" name="filename" />
      <input type="submit" value="Upload" />
    </form>
    <hr />
  </v-container>
</template>

<script>
import { mapGetters } from "vuex";
const staticData = require("../static.json");

export default {
  components: {},
  data() {
    const categories = Object.keys(staticData);
    const category = categories[0];
    const subCategory = Object.keys(staticData[category])[0];

    return {
      categories,
      subCategory,
      category,
      staticData,
      collapsed: this.$vuetify.breakpoint.smAndDown,
    };
  },
  computed: { ...mapGetters(["loggedInUser"]) },
  middleware: "auth",
  methods: {
    // Send a request to the API to delete a category.
    DeleteCategory(menuCategory) {},
    // Send a request to the API to delete a subcategory from a category.
    DeleteSubcategory(menuCategory, menuSubCategory) {},
  },
};
</script>