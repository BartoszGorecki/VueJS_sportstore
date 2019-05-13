<template>
  <div class="row mt-2">
    <div class="col form-group">
      <select class="form-control" @change="changePageSize">
        <option value="4">4 per page</option>
        <option value="8">8 per page</option>
        <option value="12">12 per page</option>
      </select>
    </div>
    <div class="text-right col" v-show="showPagination">
      <div class="btn-group mx-2">
        <button
          v-for="i in pageNumbers"
          :key="i"
          class="btn"
          :class="i === currentPage ? 'btn-primary' : 'btn-secondary'"
          @click="setCurrentPage(i)"
        >{{ i }}</button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState, mapGetters, mapMutations } from "vuex";

export default {
  computed: {
    ...mapState(["currentPage"]),
    ...mapGetters(["pageCount", "showPagination"]),
    pageNumbers() {
      return [...Array(this.pageCount + 1).keys()].slice(1);
    }
  },
  methods: {
    ...mapMutations(["setCurrentPage", "setPageSize"]),
    changePageSize(e) {
      this.setPageSize(+e.target.value);
    }
  }
};
</script>