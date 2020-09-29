<template>
  <v-app>
    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="8">
            <v-card class="elevation-12">
              <v-window v-model="step">
                <v-window-item :value="1">
                  <v-row>
                    <v-col cols="12" md="8">
                      <v-card-text class="mt-12">
                        <v-img
                          :src="require('../assets/logo.svg')"
                          class="my-3"
                          contain
                          height="40"
                        />
                        <h2 class="text-center display-1 text--accent-3" style="color:#3bb249;">Sign in</h2>
                        <div class="text-center" mt-4>
                          <v-btn class="mx-2" fab color="black" outlined>
                            <v-icon>fab fa-facebook-f</v-icon>
                          </v-btn>
                          <v-btn class="mx-2" fab color="black" outlined>
                            <v-icon>fab fa-google-plus-g</v-icon>
                          </v-btn>
                          <v-btn class="mx-2" fab color="black" outlined>
                            <v-icon>fab fa-linkedin-in</v-icon>
                          </v-btn>
                        </div>
                          <v-form ref="login" v-model="valid" lazy-validation>
                            <v-text-field
                              label="Email"
                              name="Email"
                              prepend-icon="email"
                              type="text"
                              color="#3bb249" 
                              :rules="emailRules"
                              v-model="loginEmail"
                              required />
                            <v-text-field
                              id="password"
                              label="Password"
                              name="Password"
                              prepend-icon="lock"
                              type="password"
                              color="#3bb249" 
                              :rules="passwordRules"
                              v-model="loginPassword"
                              required />
                          </v-form>
                          <h3 class="text-center mt-1" style="color:#3bb249;"> Forgot your password?</h3>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn @click="login" rounded color="#3bb249" dark> LOGIN</v-btn>
                      </div>
                    </v-col>
                    <v-col cols="12" md="4" style="background-color:#3bb249;">
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center display-1">Hello Friend !</h1>
                        <h5 class="text-center">Enter your personal information in order to access our content</h5>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn rounded outlined="" dark @click="step++">SIGN UP</v-btn>
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>
                <v-window-item :value="2">
                  <v-row class="fill-height">
                    <v-col cols="12" md="4" style="background-color:#3bb249;">
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center display-1">Welcome Back !</h1>
                        <h5 class="text-center">Login in to access our content</h5>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn rounded outlined dark @click="step--">LOGIN</v-btn>
                      </div>
                    </v-col>
                    <v-col cols="12" md="8">
                      <v-card-text class="mt-12">
                        <h1 class="text-center display-1 text--accent-3" style="color:#3bb249;">Create Account</h1>
                        <div class="text-center mt-4">
                          <v-btn class="mx-2" fab color="black" outlined>
                            <v-icon>fab fa-facebook-f</v-icon>
                          </v-btn>
                          <v-btn class="mx-2" fab color="black" outlined>
                            <v-icon>fab fa-google-plus-g</v-icon>
                          </v-btn>
                          <v-btn class="mx-2" fab color="black" outlined>
                            <v-icon>fab fa-linkedin-in</v-icon>
                          </v-btn>
                        </div>
                        <v-form  ref="signup" v-model="valid" lazy-validation>
                          <v-text-field
                            label="Name"
                            name="Name"
                            prepend-icon="person"
                            type="text"
                            color="#3bb249" 
                            :rules="nameRules"
                            />
                          <v-text-field
                            label="Email"
                            name="Email"
                            prepend-icon="email"
                            type="text"
                            color="#3bb249"
                            :rules="emailRules"
                            v-model="signupEmail"
                            />
                          <v-text-field
                            id="password"
                            label="Password"
                            name="Password"
                            prepend-icon="lock"
                            type="password"
                            color="#3bb249" 
                            :rules="signupPasswordRules"
                            v-model="signupPassword"
                            />
                            <v-checkbox
                              v-model="checkbox"
                              :rules="[v => !!v || 'You must agree to continue!']"
                              label="Agree to terms"
                              type="checkbox"
                              color="#3bb249" 
                            ></v-checkbox>
                        </v-form>
                      </v-card-text>
                      <div class="text-center mt-n5">
                        <v-btn :disabled="!valid" @click="signup" rounded color="#3bb249" dark>SIGN UP</v-btn>
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>
                <v-window-item :value="3">
                  <v-img
                    :src="require('../assets/logo.svg')"
                    height="200"
                    contain
                  />
                </v-window-item>
              </v-window>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>
<script>
export default {
  data: () => ({
    step: 1,
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+/.test(v) || 'E-mail must be valid',
    ],
    nameRules: [
      v => !!v || 'Name is required'
    ],
    passwordRules: [
      v => !!v || 'Wrong password'
    ],
    signupPasswordRules: [
      v => !!v || 'Password is required'
    ],
    checkbox: false,
    valid: true,
    // store the user data
    signupEmail: '',
    signupPassword: '',
    loginEmail: '',
    loginPassword: '',
    savedEmail: '',
    savedPassword: ''
  }),
  methods: {
    signup () {
      this.$refs.signup.validate();
      //If form validation is true, save email and password
      if (this.$refs.signup.validate()) {
        this.savedEmail = this.signupEmail;
        this.savedPassword = this.signupPassword;
        this.step = 1
      }
    },
    login () {
      this.$refs.login.validate();
      //If form validation is true, compare email and password with saved email and saved password
      if (this.$refs.login.validate()) {
        if (this.loginEmail === this.savedEmail && this.loginPassword === this.savedPassword ){
          this.step = 3
        } else {
          this.loginPassword = ''
        }
      }

    }
  },
  props: {
    source: String
  }
}
</script>