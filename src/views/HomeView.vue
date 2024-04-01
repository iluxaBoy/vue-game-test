<script setup>
// import { routerLink } from "vue-router";
import { ref } from "vue";
import useVuelidate from "@vuelidate/core";
import { required, minLength, email } from "@vuelidate/validators";

let link = ref(false);

const formData = ref({
  email: "",
  password: "",
});

const rules = {
  email: { required, email },
  password: { required, minLength: minLength(6) },
};

const v$ = useVuelidate(rules, formData);

const submitForm = async () => {
  const result = await v$.value.$validate();
  if (result) {
    window.location.href = "/game";
  }
};
</script>

<template>
  <v-container>
    <div class="d-flex align-center flex-column">
      <v-card variant="tonal">
        <v-card-title>Login</v-card-title>
        <v-sheet theme="dark" class="mx-auto" width="300">
          <v-form fast-fail @submit.prevent="submitForm">
            <v-text-field v-model="formData.email" label="Email"></v-text-field>
            <v-alert
              color="error"
              variant="outlined"
              v-for="error in v$.email.$errors"
              :key="error.$uid"
            >
              {{ error.$message }}
            </v-alert>

            <v-text-field
              v-model="formData.password"
              label="Password"
              type="password"
            ></v-text-field>
            <v-alert
              color="error"
              variant="outlined"
              v-for="error in v$.password.$errors"
              :key="error.$uid"
            >
              {{ error.$message }}
            </v-alert>

            <v-btn class="mt-2" type="submit" block>Login </v-btn>
          </v-form>
        </v-sheet>
      </v-card>
    </div>
  </v-container>
</template>

<style scoped lang="scss">
.v-container {
  margin-top: 125px;
}
</style>
