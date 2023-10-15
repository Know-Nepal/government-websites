<template>
  <div id="app">
    <h1 class="title">Government Websites</h1>
    <h2 class="subtitle">Powered by Know Nepal</h2>
    <div class="search-bar">
      <input type="text" v-model="searchQuery" placeholder="Search by name" />
    </div>
    <div class="websites-container">
      <government-website v-for="website in filteredAndPaginatedWebsites" :key="website.name" :website="website" />
    </div>
    <div class="pagination">
      <button @click="previousPage" :disabled="currentPage === 1">Previous</button>
      <span>Page {{ currentPage }} of {{ totalPages }}</span>
      <button @click="nextPage" :disabled="currentPage === totalPages">Next</button>
    </div>
  </div>
</template>

<script>
import GovernmentWebsite from "./components/Websites.vue";
import websitesData from "../data/websites.json";

export default {
  components: {
    GovernmentWebsite,
  },
  data() {
    return {
      websites: websitesData.items,
      searchQuery: "",
      currentPage: 1,
      websitesPerPage: 8, 
    };
  },
  computed: {
    filteredAndPaginatedWebsites() {
      const filteredWebsites = this.websites.filter(website =>
        website.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
      const startIndex = (this.currentPage - 1) * this.websitesPerPage;
      const endIndex = startIndex + this.websitesPerPage;
      return filteredWebsites.slice(startIndex, endIndex);
    },
    totalPages() {
      const filteredWebsites = this.websites.filter(website =>
        website.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
      return Math.ceil(filteredWebsites.length / this.websitesPerPage);
    },
  },
  methods: {
    previousPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Arial", sans-serif;
  text-align: center;
  color: #4caf50;
}

.title {
  color: #4caf50;
}

.subtitle {
  color: #fff;
}

.search-bar {
  margin-bottom: 20px;
}

input {
  padding: 10px;
  font-size: 16px;
  width: 300px;
  border: 1px solid #fff;
  border-radius: 5px;
}

.websites-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.pagination {
  margin-top: 20px;
}

.pagination button {
  margin: 0 10px;
  cursor: pointer;
  padding: 10px 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 25px;
  transition: background-color 0.3s ease;
}

.pagination button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>
