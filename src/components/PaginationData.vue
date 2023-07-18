<template>
  <div id="pagination">
    <button id="prevBtn" @click="$emit('prevPage')" :disabled="currentPage === 1">Previous</button>

    <span
      v-for="pageNumber in displayedPageNumbers"
      :key="pageNumber"
      :class="{ 'page-number': true, 'active': pageNumber === currentPage, 'ellipsis': pageNumber === '...' }"
      @click="$emit('goToPage', pageNumber)" >
      {{ pageNumber }}
    </span>

    <button id="nextBtn" @click="$emit('nextPage')" :disabled="currentPage === totalPages">Next</button>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true
    },
    totalPages: {
      type: Number,
      required: true
    }
  },
  computed: {
    displayedPageNumbers() {
      let rangeStart = Math.max(1, this.currentPage - 1);
      let rangeEnd = Math.min(rangeStart + 2, this.totalPages);

      if (rangeEnd - rangeStart < 2) {
        rangeStart = Math.max(1, rangeEnd - 2);
      }

      const pageNumbers = [];

      for (let i = rangeStart; i <= rangeEnd; i++) {
        pageNumbers.push(i);
      }

      if (rangeEnd < this.totalPages - 2) {
        pageNumbers.push('...', this.totalPages - 2, this.totalPages - 1, this.totalPages);
      }

      return pageNumbers;
    }
  }
};
</script>

<style>
        th, td {
            border: 2px solid black;
            cursor: pointer;
            border-collapse: collapse;
        }

        img {
            height: 100px;
            width: 100px;
        }

        #pagination {
            display: flex;
            justify-content: center;
            margin-top: 20px;
        }

        #pagination button {
            margin: 0 5px;
            padding: 5px 10px;
        }

        #pagination .page-number {
            display: inline-block;
            margin: 0 5px;
            padding: 5px;
            cursor: pointer;
        }

        #pagination .page-number.active {
            background-color: #878484;
        }

        #pagination .page-number.ellipsis {
            padding: 0 5px;
        }
</style>


 