<template>
  <div class="m-2">
    <h4 class="bg-primary text-white text-center p-2">SportsStore Administration</h4>
    <h4
      v-if="showFailureMessage"
      class="bg-danger text-white text-center p-2 my-2"
    >Authentication Failed. Please try again.</h4>
    <div class="form-group">
      <input-area
        label="username"
        :validation="$v.username"
        :value="$v.username.$model"
        @input="$v.username.$model = $event"
      />
    </div>
    <div class="form-group">
      <input-area
        label="password"
        :validation="$v.password"
        :value="$v.password.$model"
        @input="$v.password.$model = $event"
      />
    </div>
    <div class="text-center">
      <button class="btn btn-primary" @click="handleAuth">Log In</button>
    </div>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
import { mapActions, mapState } from "vuex";
import InputArea from "../Input";

export default {
  components: { InputArea },
  data: function() {
    return {
      username: "admin",
      password: "secret",
      showFailureMessage: false
    };
  },
  computed: {
    ...mapState({ authenticated: state => state.auth.authenticated })
  },
  validations: {
    username: { required },
    password: { required }
  },
  methods: {
    ...mapActions(["authenticate"]),
    async handleAuth() {
      this.$v.$touch();
      if (!this.$v.$invalid) {
        await this.authenticate({
          name: this.username,
          password: this.password
        });
        if (this.authenticated) {
          this.$router.push("/admin");
        } else {
          this.showFailureMessage = true;
        }
      }
    }
  }
};
</script>