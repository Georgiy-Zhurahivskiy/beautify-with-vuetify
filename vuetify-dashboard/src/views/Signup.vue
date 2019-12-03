<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>Signup</h1>
        <v-form ref="signUpForm" v-model="formValidity">
          <v-text-field label="Email" type="email" v-model="email" :rules="emailRules" required></v-text-field>
          <v-autocomplete label="Which browser do you use?" :items="browsers"></v-autocomplete>
          <v-file-input label="Attach profile picture"></v-file-input>
          <v-text-field v-model="birthday" label="Birthday" readonly></v-text-field>
          <v-date-picker v-model="birthday"></v-date-picker>
          <v-checkbox
            label="Agree to terms & conditions"
            v-model="aggreToTerms"
            :rules="aggreToTermsRules"
            required
          ></v-checkbox>
          <v-btn class="mr-4" color="success" @click="validateForm">Validate form</v-btn>
          <v-btn class="mr-4" :disabled="!formValidity" type="submit" color="primary">Submit</v-btn>
          <v-btn class="mr-4" color="warning" @click="resetValidation">Reset validation</v-btn>
          <v-btn color="error" @click="reset">Reset</v-btn>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    formValidity: false,
    birthday: "",
    email: "",
    browsers: ["Chrome", "Firefox", "Safari", "Edge", "Brave"],
    aggreToTerms: false,
    aggreToTermsRules: [
      value =>
        !!value ||
        "You must agree to the terms and conditions to sign up for an acconunt."
    ],
    emailRules: [
      value => !!value || "Email is required.",
      value => value.indexOf("@") !== 0 || "Email should have a username.",
      value =>
        value.includes("@") || "Email should should include and @ symbol.",
      value =>
        value.indexOf(".") - value.indexOf("@") > 1 ||
        "Email should contain a valid domain.",
      value =>
        value.indexOf(".") <= value.length - 3 ||
        "Email should contain a valid domain extension."
    ]
  }),
  methods: {
    resetValidation() {
      this.$refs.signUpForm.resetValidation();
    },
    reset() {
      this.$refs.signUpForm.reset();
    },
    validateForm() {
      this.$refs.signUpForm.validate();
    }
  }
};
</script>
