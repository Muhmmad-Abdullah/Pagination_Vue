<template>
  <div>
    <DataTable :data="pageData" :config="config" />
    <PaginationData
      :currentPage="currentPage"
      :totalPages="totalPages"
      @prevPage="prevPage"
      @nextPage="nextPage"
      @goToPage="goToPage"
    />
  </div>
</template>

<script>
import DataTable from './components/DataTable.vue';
import PaginationData from './components/PaginationData.vue';

export default {
  components: {
    DataTable,
    PaginationData
  },
  data() {      
    return {
      config: [
        { key_obj: "albumId", label_key: "Albums", type: "text" },
        { key_obj: "id", label_key: "ID Number", type: "text" },
        { key_obj: "title", label_key: "Title", type: "text" },
        { key_obj: "url", label_key: "Image 1", type: "img" },
        { key_obj: "thumbnailUrl", label_key: "Image 2", type: "img" },
      ],
      currentPage: 1,
      pageData: [],
      totalPages: 500,
      itemsPerPage: 10,
    };
  },
  methods: {
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    fetchData() {
      fetch("https://jsonplaceholder.typicode.com/photos")
        .then((response) => response.json())
        .then((fetchedData) => {
          this.pageData = fetchedData;
          this.totalPages = Math.ceil(this.pageData.length / this.itemsPerPage);
        })
        .catch((error) => {
          console.log("Cannot fetch data:", error);
        });
    },
    goToPage(pageNumber) {
      if (pageNumber === '...') return;

      this.currentPage = pageNumber;
    },
  },
  created() {
    this.fetchData();
  },
};
</script>


