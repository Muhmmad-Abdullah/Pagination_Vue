<template>
  <table>
    <thead>
      <tr>
        <th v-for="item in config" :key="item.key_obj">
          {{ item.label_key }}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="row in currentPageData" :key="row.id">
        <td v-for="item in config" :key="item.key_obj">
          <template v-if="item.type === 'img'">
            <img :src="row[item.key_obj]" :alt="item.label_key" />
          </template>
          <template v-else>
            {{ row[item.key_obj] }}
          </template>
        </td>
      </tr>
    </tbody>
  </table>
</template>
<script>
export default {
  props: {
    data: {
      type: Array,
      required: true
    },
    config: {
      type: Array,
      required: true
    }
  },
  computed: {
    currentPageData() {
      const startIndex = (this.$parent.currentPage - 1) * this.$parent.itemsPerPage;
      const endIndex = this.$parent.currentPage * this.$parent.itemsPerPage;
      return this.data.slice(startIndex, endIndex);
    }
  }
};
</script>


