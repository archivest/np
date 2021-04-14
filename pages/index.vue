<template>
  <v-container>
    <v-toolbar id="appBar" dense class="pa-0 mx-auto">
      <v-app-bar-nav-icon
        v-show="$vuetify.breakpoint.smAndDown"
        @click="showAccordionMenu = !showAccordionMenu"
      ></v-app-bar-nav-icon>
      <v-toolbar-items class="hidden-sm-and-down">
        <v-menu
          v-for="menuCategory in categories"
          :key="menuCategory"
          open-on-hover
          rounded
          :close-on-content-click="false"
          class="categoryMenu"
        >
          <template #activator="{ on, attrs }" class="hidden-md-and-up">
            <v-btn
              color="secondary"
              v-bind="attrs"
              text
              class="ml-10"
              v-on="on"
            >
              {{ menuCategory }}
            </v-btn>
          </template>

          <v-list rounded>
            <v-list-item
              v-for="menuSubCategory in Object.keys(staticData[menuCategory])"
              :key="menuSubCategory"
            >
              <v-list-item-title
                @click="changePhotos(menuCategory, menuSubCategory)"
              >
                {{ menuSubCategory }}
              </v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-toolbar-items>
    </v-toolbar>
    <div v-show="showAccordionMenu">
      <v-expansion-panels accordion focusable>
        <v-expansion-panel
          v-for="menuCategory in categories"
          :key="menuCategory"
        >
          <v-expansion-panel-header>{{
            menuCategory
          }}</v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-list>
              <v-list-item
                v-for="menuSubCategory in Object.keys(staticData[menuCategory])"
                :key="menuSubCategory"
              >
                <v-list-item-title
                  @click="changePhotos(menuCategory, menuSubCategory)"
                >
                  {{ menuSubCategory }}
                </v-list-item-title>
              </v-list-item>
            </v-list>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </div>
    <client-only>
      <stack
        v-show="loaded"
        :column-min-width="500"
        :column-min-height="500"
        monitor-images-loaded
        class="mt-2"
      >
        <stack-item v-for="(photo, photoindex) in photos" :key="photoindex">
          <img
            :src="photo"
            alt="photo"
            @click="index = photoindex"
            @load="!loadedPhotos.includes(photo) && loadedPhotos.push(photo)"
          />
        </stack-item>
      </stack>
    </client-only>
    <vue-loading
      v-show="!loaded"
      class="loader"
      type="spin"
      color="#5ac1dd"
      :size="{ width: '16%', height: '16%' }"
    ></vue-loading>
    <div v-show="!loaded" id="loader" />
    <CoolLightBox :items="photos" :index="index" @close="index = null">
    </CoolLightBox>
  </v-container>
</template>

<script>
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
      index: null,
      loadedPhotos: [],
      staticData,
      showAccordionMenu: false,
      collapsed: this.$vuetify.breakpoint.smAndDown,
    };
  },
  computed: {
    photos() {
      return staticData[this.category][this.subCategory];
    },
    loaded() {
      const photos = this.photos;

      return photos.every((photo) => this.$data.loadedPhotos.includes(photo));
    },
  },
  methods: {
    changePhotos(menuCategory, menuSubCategory) {
      this.category = menuCategory;
      this.subCategory = menuSubCategory;
    },
  },
};
</script>

<style scoped>
.loader {
  margin: auto;
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
}

img {
  margin: 0;
  width: 100%;
  height: auto;
}

#appBar {
  display: flex;
  justify-content: center;
}

@media screen and (max-width: 600px) {
  #appBar {
    height: auto !important;
  }
}

.categoryMenu {
  flex: 1;
}
</style>
