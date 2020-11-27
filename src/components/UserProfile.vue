<template>
  <div class="p-4">
    <b-form @submit="onSubmit" v-if="show">
      <b-form-group id="firstname" label="First name:" label-for="firstname">
        <b-form-input
          id="firstname"
          v-model="form.firstName"
          type="text"
          required
          placeholder="Enter first name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="lastname" label="Last name:" label-for="lastname">
        <b-form-input
          id="lastname"
          v-model="form.lastName"
          type="text"
          required
          placeholder="Enter last name"
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="phonenumber"
        label="Phonenumber:"
        label-for="phonenumber"
      >
        <b-form-input
          id="phonenumber"
          v-model="form.phoneNumber"
          type="text"
          placeholder="Enter first name"
        ></b-form-input>
      </b-form-group>
      <span class="float-right">
        <b-button
          @click="$emit('hide-modal')"
          class="mr-2"
          variant="outline-secondary"
          >Cancel</b-button
        >
        <b-button type="submit" variant="primary">Save</b-button>
      </span>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        email: "",
        firstName: "",
        lastName: "",
        phoneNumber: "",
      },
      show: true,
    };
  },
  mounted:function(){
      console.log("mounted")
      if(localStorage && localStorage.getItem('userData')){
          this.form=JSON.parse(localStorage.getItem('userData'))
      }
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
     // alert(JSON.stringify(this.form));
      localStorage.setItem("userData",JSON.stringify(this.form));
      this.$emit('hide-modal');
      this.$emit('show-toaster')
    },
  },
};
</script>