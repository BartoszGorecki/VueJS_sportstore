<template>
  <div class="container-fluid">
    <div class="row my-2" v-for="c in categories" :key="c">
      <button
        class="btn btn-block"
        @click="setCurrentCategory(c)"
        :class="c === currentCategory
 ? 'btn-primary' : 'btn-secondary'"
      >
        {{ c }}
        <small>({{ productsPerCategories(c) }})</small>
      </button>
    </div>
  </div>
</template>

<script>
import { mapState, mapGetters, mapMutations } from "vuex";

export default {
  computed: {
    ...mapState(["currentCategory"]),
    ...mapGetters(["categories"])
  },
  methods: {
    ...mapMutations(["setCurrentCategory"]),
    productsPerCategories(c) {
      return c === "All"
        ? this.$store.state.products.length
        : this.$store.state.products.filter(product => product.category == c)
            .length;
    }
  }
};
</script>