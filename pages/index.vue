<script>
export default {
 
  data() {
    return {
      validationStatus: false,
      darkmode: false,
      show1: false,
      password: '',
      username: '',
      rules: {
        required: value => !!value || 'Required.',
        min: v => v.length >= 8 || 'Min 8 characters',
        emailMatch: () => (`The username and password you entered don't match`),
      },
    }
  },

   methods: {
  darkMode() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },
    submitForm(){
      if( this.username == "StoreSpy" && this.password == "storespy59"){
        this.validationStatus = false,
        this.$router.push("/dashboard");
      }  
      else {
         this.validationStatus = true
      }
    },
  },
}
</script>

<template>
  <v-form>
    <v-container fluid>
      <v-row>
        <v-col style="position: absolute; right: 0;">
          <v-btn @click="darkMode">
            <v-icon class="mr-2">
              mdi-brightness-4
            </v-icon>
          </v-btn>
        </v-col>

        <v-col
          cols="12"
          class="form_login"
        >
          <v-card>
            <v-card-title>
              Login Page
            </v-card-title>

            <v-text-field
              style="margin: 3%"
              v-model="username"
              label="Username"
            ></v-text-field>

            <v-text-field
              style="margin: 3%"
              v-model="password"
              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min]"
              :type="show1 ? 'text' : 'password'"
              name="input-10-1"
              label="Password"
              hint="At least 8 characters"
              counter
              @click:append="show1 = !show1"
            ></v-text-field>
            <v-btn
              @click="submitForm"
              style="margin: 3%"
              color="primary"
            >Submit</v-btn>
            <v-alert
              v-if="validationStatus"
              dense
              outlined
              type="error"
            >
              Invalid <strong>username</strong> or <strong>password</strong>
            </v-alert>
          </v-card>

        </v-col>

      </v-row>
    </v-container>
  </v-form>
</template>

<style scoped>
.form_login {
    left      : 50%;
    top       : 50%;
    position  : absolute;
    transform : translate(-50%, -50%);
    max-width: 50%; 
    padding: 5%;
    float: inline-end;
}
</style>
