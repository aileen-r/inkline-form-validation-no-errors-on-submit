<template>
  <h1>Inkline Form Errors</h1>
  <p>Try submitting the empty form.</p>
  <i-form v-model="form" @submit="submit">
    <i-form-group>
      <i-form-label for="email">Email Address</i-form-label>
      <i-input name="email" type="email" />
      <i-form-error for="email" :visible="['invalid', 'touched']" />
    </i-form-group>
    <i-form-group>
      <i-form-label for="password">Password</i-form-label>
      <i-input name="password" type="password" />
      <i-form-error for="password" :visible="['invalid', 'touched']" />
    </i-form-group>
    <i-form-group>
      <i-button block color="primary" type="submit">Log In</i-button>
    </i-form-group>
  </i-form>
  <p>
    Both of these inputs are required, blocking the form submit, but no error
    feedback is shown.
  </p>
</template>

<script>
export default {
  name: "InklineForm",
  data() {
    const schema = {
      email: {
        validators: [
          {
            name: "required",
          },
          {
            name: "email",
          },
        ],
      },
      password: {
        validators: [
          {
            name: "required",
          },
        ],
      },
    };
    return {
      form: this.$inkline.form(schema),
    };
  },
  methods: {
    submit(payload) {
      // I would expect this to be called when clicking "log in"
      if (payload.invalid) {
        // Then I could set fields to touched so that error messages appear
        this.form.touched = true;
      }
    },
  },
};
</script>

<style>
.form {
  max-width: 500px;
  margin: 0 auto;
}
</style>