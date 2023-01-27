<template>
  <q-page class="flex flex-center">
    <div class="container">
      <ais-instant-search :search-client="searchClient" index-name="back4blood">
        <div class="search-panel__filters">
          <span>Type</span>
          <ais-refinement-list attribute="Type" />
          <span>Affinity</span>
          <ais-refinement-list attribute="Card_Affinity" />
          <span>Team Effect</span>
          <ais-refinement-list attribute="Team_Effect" />
          <span>Category</span>
          <ais-refinement-list attribute="Deck_Category" />
        </div>
        <div class="search-panel__results">
          <ais-search-box />
          <ais-hits>
            <template v-slot:item="{ item }">
              <div>
                <div class="hit-name">
                  <ais-highlight :hit="item" attribute="name" />
                </div>
                <img :src="item.Image_Url" align="left" :alt="item.Image_Url" />
                <div class="hit-description">
                  <ais-snippet :hit="item" attribute="Effect Description" />
                </div>
                <div class="hit-info">Team Effect: {{ item.team_effect }}</div>
                <div class="hit-info">Damage Type: {{ item.damage_type }}</div>
              </div>
            </template>
          </ais-hits>
          <ais-configure
            :attributesToSnippet="['type:50']"
            snippetEllipsisText="…"
          />
        </div>
        <ais-pagination />
      </ais-instant-search>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import { instantMeiliSearch } from "@meilisearch/instant-meilisearch";

export default defineComponent({
  name: "IndexPage",
  data() {
    return {
      searchClient: instantMeiliSearch(
        "https://index.weeumson.com",
        "MmUwNGZkYmEwNjQ4NzdiYWVkNmEzODU0"
      ),
      search: ref(""),
    };
  },
});
</script>
<style>
body,
h1 {
  margin: 0;
  padding: 0;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
    Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}

.ais-Hits-item {
  margin-bottom: 1em;
  width: calc(50% - 1rem);
}

.ais-Hits-item img {
  margin-right: 1em;
  width: 100%;
  height: 100%;
  margin-bottom: 0.5em;
}

.ais-Highlight-highlighted {
  background: cyan;
  font-style: normal;
}

.disclaimer {
  margin-left: 1em;
}

.hit-name {
  margin-bottom: 0.5em;
}

.hit-info {
  font-size: 90%;
}

.header {
  display: flex;
  align-items: center;
  min-height: 50px;
  padding: 0.5rem 1rem;
  background-image: linear-gradient(to right, #4dba87, #2f9088);
  color: #fff;
  margin-bottom: 1rem;
}

.header-title {
  font-size: 1.2rem;
  font-weight: normal;
}

.hit-description {
  font-size: 90%;
  margin-bottom: 0.5em;
  color: grey;
}

.header-title::after {
  content: " ▸ ";
  padding: 0 0.5rem;
}

.header-subtitle {
  font-size: 1.2rem;
}

.container {
  padding: 1rem;
}

.ais-InstantSearch {
  max-width: 960px;
  overflow: hidden;
  margin: 0;
}

.search-panel__filters {
  float: left;
  width: 200px;
}

.search-panel__results {
  margin-left: 210px;
}

.ais-SearchBox {
  margin-bottom: 2rem;
}

.ais-Pagination {
  margin: 2rem auto;
  text-align: center;
}
.ais-SearchBox-form {
  margin-bottom: 20px;
}
</style>
