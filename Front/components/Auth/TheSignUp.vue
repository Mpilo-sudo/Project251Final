<template>
      <v-form ref="form" v-model="valid" lazy-validation>
            <v-container>
                  <v-container>
                        <v-text-field
                              filled
                              dense
                              label="Email"
                              v-model="signUp.email"
                        ></v-text-field>
                        <v-text-field
                              filled
                              dense
                              label="Password"
                              v-model="signUp.password"
                        ></v-text-field>
                        <v-text-field
                              filled
                              dense
                              label="Confirm Password"
                              v-model="signUp.confirmPassword"
                        ></v-text-field>
                  </v-container>
                  <v-container id="buttonsForm">
                        <v-btn
                              :disabled="!valid"
                              color="success"
                              outlined
                              class="mr-2"
                              @click="validate()"
                        >
                              Sign Up
                        </v-btn>

                        <v-btn
                              color="error"
                              class="mr-2"
                              outlined
                              @click="reset"
                        >
                              Cancel
                        </v-btn>
                        <v-btn
                              color="primary"
                              outlined
                              @click="$emit('toggle')"
                        >
                              Log IN
                        </v-btn>
                  </v-container>
            </v-container>
      </v-form>
</template>
<script>
export default {
      data() {
            return {
                  date: new Date(
                        Date.now() - new Date().getTimezoneOffset() * 60000
                  )
                        .toISOString()
                        .substr(0, 10),
                  modal: false,
                  signUp: {
                        email: '',
                        password: '',
                        confirmPassword: '',
                  },
            }
      },
      methods: {
            setSignUp() {
                  this.signUp.birthDate = this.date
                  if (this.signUp.confirmPassword === this.signUp.password){
                        this.$store.commit("authModule/setSignDetails", this.signUp)
                  }
                  else{
                        alert("Your passwords do not match");
                  }

            },
            validate() {
                  this.$store.commit("authModule/toggleLogin", false)
                  this.$store.commit("authModule/setEmail", this.email)
                  this.setSignUp()
                  this.$store.dispatch("authModule/authenticateUser");
                  this.$router.push('/Client/')

            },
            reset() {
                  this.$refs.form.reset()
                  this.$store.commit("authModule/resetSignDetails")
                  this.$router.push('/')
            },
      },
}
</script>
<style lang=""></style>
