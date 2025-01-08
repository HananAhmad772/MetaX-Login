<template>
  <v-responsive
    class="align-centerfill-height mx-auto"
    max-width="1500"
  >
    <v-row>
      <v-col cols="16">
        <div class="header">
          <v-img
            class="mb-6"
            width="250"
            height="85"
            src="@/assets/logo-update.png"
          />
        </div>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="3">
        <v-card class="login-card">
          <svg-icon type="mdi" :path="path" class="icon"></svg-icon>
          <div class="login-heading">
            <h4>Login</h4>
            <p>To access your account please enter your email and password.<br><br>
              If you are having problems signing in please click 'Forgot password?' and follow the instructions.
            </p>
          </div>
        </v-card>
      </v-col>
      <v-col cols="4">
        <div class="welcome-back">
          <h1>Welcome back</h1>
        </div>
        <form @submit.prevent="submit">
          <v-sheet class="mx-auto">
            <v-form fast-fail>
              <!-- Email Field -->
              <v-text-field
                v-model="email.value"
                :error-messages="email.error"
                label="Email"
                name="email"
                required
              ></v-text-field>

              <!-- Password Field -->
              <v-text-field
                v-model="password.value"
                :error-messages="password.error"
                label="Password"
                type="password"
                required
              ></v-text-field>

              <!-- Submit Button -->
              <v-btn class="button mt-2" type="submit" block>Login</v-btn>
            </v-form>
            <br>
            <div class="forgot-reg">
              <a href="" class="forgot-password">Forgot your password?</a>
              <br><br>
              <p>Did not have an account?  <a href="" class="forgot-password">Register now</a></p>
            </div>
          </v-sheet>
        </form>
      </v-col>
    </v-row>
  </v-responsive>
</template>

<script setup>
import { ref } from 'vue';
import { useField, useForm } from 'vee-validate';
import SvgIcon from '@jamescoyle/vue-icon';
import { mdiArrowRight } from '@mdi/js';

// Form validation
const { handleSubmit } = useForm({
  validationSchema: {
    email(value) {
      if (/^[a-z.-]+@[a-z.-]+\.[a-z]+$/i.test(value)) return true;
      return 'Must be a valid e-mail.';
    },
    password(value) {
      if (value.length < 8) return 'Password must be at least 8 characters long.';
      if (!/[A-Z]/.test(value)) return 'Password must contain at least one uppercase letter.';
      if (!/[0-9]/.test(value)) return 'Password must contain at least one number.';
      if (!/[\W_]/.test(value)) return 'Password must contain at least one special character.';
      return true;
    },
  },
});

// Using useField to manage form fields
const email = useField('email');
const password = useField('password');

// SVG icon
const path = ref(mdiArrowRight);

// Form submit handler
const submit = handleSubmit(values => {
  alert(JSON.stringify(values, null, 2));
});
</script>
<playground-resources lang="json">
  {
    "imports": {
      "vee-validate": "https://cdn.jsdelivr.net/npm/vee-validate@4.8.4/dist/vee-validate.esm.js",
      "@vue/devtools-api": "https://cdn.jsdelivr.net/npm/@vue/devtools-api@6.5.0/lib/esm/index.js"
    }
  }
</playground-resources>

<style scoped>
.header {
  width: 100%;
  height: 120px;
  padding: 15px;
  box-shadow: 0px 2px 2px rgba(0, 0, 0, 0.1);
}
.login-card{
  max-width: 300px;
  min-height: 100vh;
  padding: 45px;
  font-size: 13px;
  display: flex;
  background-color: #FAFAFA;
  margin-top: 0;
}
.login-card h4{
  font-size: 22px;
  margin-bottom: 10px;
  padding-left: 2px;
  font-weight: 400;
}
.icon{
  width: 100px; 
  margin-top: 4px;
}
.welcome-back{
  font-size: 17px;
  margin-top: 30px;
}
.welcome-back h1{
  font-weight: 500;
  margin-bottom: 45px;
}
.button{
  background-color: rgb(143, 39, 199);
  color: white;
}
.forgot-password{
  color: rgb(80, 80, 80);
}
.forgot-reg{
  text-align: center;
}
</style>
