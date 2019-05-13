<template>
  <div>
    <div class="container-fluid">
      <div class="row">
        <div class="col bg-dark text-white">
          <a class="navbar-brand">SPORTS STORE</a>
        </div>
      </div>
    </div>
    <input-area
      v-for="(val, prop) in order"
      :key="prop"
      :label="prop"
      :validation="$v.order[prop]"
      :value="$v.order[prop].$model"
      @input="$v.order[prop].$model = $event"
    />
    <div class="text-center">
      <router-link to="/cart" class="btn btn-secondary m-1">Back</router-link>
      <button class="btn btn-primary m-1" @click="submitOrder" :disabled="$v.$invalid">Place Order</button>
    </div>
  </div>
</template>

<style>
.input-container.invalid input {
  border: 1px solid rgba(255, 0, 0, 0.6);
  box-shadow: 0 2px 4px rgba(255, 0, 0, 0.2);
}
</style>

<script>
import { required, email, numeric, minLength } from "vuelidate/lib/validators";
import InputArea from "./Input";
import { mapActions } from "vuex";

export default {
  components: { InputArea },
  data: function() {
    return {
      order: {
        name: "",
        email: "",
        address: null,
        city: null,
        zip: null
      }
    };
  },
  validations: {
    order: {
      name: { required, minLength: minLength(3) },
      email: { required, email, minLength: minLength(10) },
      address: { required, minLength: minLength(10) },
      city: { required, minLength: minLength(2) },
      zip: { required, minLength: minLength(5), numeric }
    }
  },
  methods: {
    ...mapActions({
      storeOrder: "storeOrder",
      clearCart: "cart/clearCartData"
    }),
    async submitOrder() {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        let order = await this.storeOrder(this.order);
        this.clearCart();
        this.$router.push(`/thanks/${order}`);
      }
    }
  }
};
</script>