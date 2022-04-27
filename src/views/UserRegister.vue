<template>
    <div class="col-md-12">
        <div class="card card-container">
            <h1 class="signup-title">Signup</h1>
            <img
                id="profile-img"
                src="../assets/regiter.jpg"
                alt="Cannot load the image"
                class="profile-img-card"
            />
            <Form @submit="handleRegister" :validation-schema="schema">
                <div v-if="!successful">
                    <div class="form-group">
                        <label for="username">Username</label>
                        <Field
                            name="username"
                            type="text"
                            class="form-control"
                            placeholder="Enter your username..."
                        />
                        <ErrorMessage name="username" class="error-feedback" />
                    </div>
                    <div class="form-group">
                        <label for="email">E-mail</label>
                        <Field 
                        name="email" 
                        type="email" 
                        class="form-control"
                        placeholder="Enter your email..." />
                        <ErrorMessage name="email" class="error-feedback" />
                    </div>
                    <div class="form-group">
                        <label for="password">Password</label>
                        <Field
                            name="password"
                            type="password"
                            class="form-control"
                            placeholder="Enter your password..."
                        />
                        <ErrorMessage name="password" class="error-feedback" />
                    </div>

                    <div class="form-group my-3">
                        <button
                            class="btn-register"
                            :disabled="loading"
                        >
                            <span
                                v-show="loading"
                                class="spinner-border spinner-border-sm"
                            ></span>
                            SIGN UP
                        </button>
                    </div>
                </div>
            </Form>

            <div
                v-if="message"
                class="alert"
                :class="successful ? 'alert-success' : 'alert-danger'"
            >
                {{ message }}
            </div>
        </div>
    </div>
</template>

<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";
import { mapGetters } from "vuex";

export default {
    name: "Register",
    components: {
        Form,
        Field,
        ErrorMessage,
    },
    data() {
        const schema = yup.object().shape({
            username: yup
                .string()
                .required("The username must be valid.")
                .min(3, "The username with at least 3 characters.")
                .max(20, "The username up to 20 characters."),
            email: yup
                .string()
                .required("The e-mail must be valid.")
                .email("The e-mail is not correct.")
                .max(50, "The e-mail up to 50 characters."),
            password: yup
                .string()
                .required("The password must be valid.")
                .min(6, "The password with at least 6 characters.")
                .max(40, "The password up to 20 characters.."),
        });

        return {
            successful: false,
            loading: false,
            message: "",
            schema,
        };
    },
    computed: {
        ...mapGetters([
            "userLoggedIn"
        ]),
    },
    mounted() {
        if (this.userLoggedIn) {
            this.$router.push("/profile");
        }
    },
    methods: {
        async handleRegister(user) {
            this.message = "";
            this.successful = false;
            this.loading = true;

            const [error, data] = await this.handle(
                this.$store.dispatch("register", user)
            );
            if (error) {
                console.log(error);
                this.message = "Registation failed";
                this.successful = false;
                this.loading = false;
            } else {
                this.message = data.message;
                this.successful = true;
                this.loading = false;
            }
        },
    },
};
</script>

<style>
@import "../assets/styles/main.css";
.btn-register{
    border-radius: 20px;
    border: 2px solid #000000;
    background-color: #eaea70;
    color: #000000;
    font-size: 12px;
    font-weight: bold;
    padding: 12px 45px;
    letter-spacing: 1px;
    text-transform: uppercase;
    transition: transform 80ms ease-in;
    margin-top: 10px;
    margin-left: 90px;
}
.signup-title{
    color:   #050505;
    margin-left: 100px;
    font-family: 'Acme' ;
    margin-bottom: 30px;
}
.card-container{
    
    background-color: #c1ece9;
    
}
</style>
