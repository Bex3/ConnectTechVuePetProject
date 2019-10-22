<template>
  <div class="form-wrapper">Formmmmmm
    <div class="text-xs-center" v-if="submitted">
      <h2>Thank you for you interest, we will contact you soon</h2>
      <div class="details text-xs-left">
        <h3 class="blue-grey--text">Customer details</h3>
        <p>
          <strong>Name:</strong>
          {{name}}
        </p>
        <p>
          <strong>Email:</strong>
          {{email}}
        </p>
        <p>
          <strong>Phone:</strong>
          {{phone}}
        </p>
      </div>
      <v-btn to="/">Go to homepage</v-btn>
    </div>

    <v-form v-else v-model="valid">
      <v-text-field label="Name" v-model="name" required :rules="nameRules"></v-text-field>
      <v-text-field label="Email" required :rules="emailRules" v-model="email"></v-text-field>
      <v-text-field
        label="Phone"
        required
        :rules="phoneRules"
        v-mask="'(###) ### - ####'"
        v-model="phone"
      ></v-text-field>
      <v-button @click="submit" :disabled="!valid">Submit</v-button>
    </v-form>
  </div>
</template>


<script>
import { mask } from "vue-the-mask";

export default {
  directives: {
    mask
  },
  data() {
    return {
      name: "",
      email: "",
      phone: "",
      submitted: false,
      valid: false,
      nameRules: [
        name => !!name || "Name is required",
        name => name.length > 2 || "Name must be longer than 2 characters"
      ],
      emailRules: [
        email => !!email || "Email is required",
        email =>
          /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(email) ||
          "Email must be valid"
      ],
      phoneRules: [
        phone => !!phone || "Phone is required",
        phone => phone.length >= 7 || "Phone number should be at least 7 digits"
      ]
    };
  },
  methods: {
    submit() {
      this.submitted = true;
      this.$store.dispatch("clearFavorites");
    }
  }
};
</script>

<style scoped>
.form-wrapper {
  padding: 40px;
  text-align: center;
}
.details {
  padding-top: 30px;
}
h3 {
  padding-bottom: 20px;
}
</style>