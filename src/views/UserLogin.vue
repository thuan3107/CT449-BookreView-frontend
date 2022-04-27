<template>
    <div class="col-md-12">
        <div class="card card-container">
            <h1 class="login-title">Login</h1>
            <img
                id="profile-img"
                src="../assets/login.jpg"
                alt="Cannot load the image"
                class="profile-img-card"
            />
            <Form @submit="handleLogin" :validation-schema="schema">
                <div class="form-group">
                    <label for="username">Username</label>
                    <Field name="username" type="text" class="form-control" placeholder="Enter your username..." />
                    <ErrorMessage name="username" class="error-feedback" />
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
                        class="btn-login"
                        :disabled="loading"
                    >
                        <span
                            v-show="loading"
                            class="spinner-border spinner-border-sm"
                        ></span> 
                        <span>LOG IN</span>
                    </button>
                </div>

                <div class="form-group">
                    <div v-if="message" class="alert alert-danger" role="alert">
                        {{ message }}
                    </div>
                </div>
            </Form>
        </div>
    </div>
</template>

<script>
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";
import { mapGetters} from "vuex";

export default {
    name: "Login",
    components: {
        Form,
        Field,
        ErrorMessage,
    },
    data() {
        const schema = yup.object().shape({
            username: yup.string().required("The username should be a valid."),
            password: yup.string().required("The email should be a valid address."),
        });

        return {
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
    created() {
        if (this.userLoggedIn) {
            this.$router.push("/profile");
        }
    },
    methods: {
        async handleLogin(user) {
            this.loading = true;

            const [error] = await this.handle(
                this.$store.dispatch("login", user)
            );
            if (error) {
                console.log(error);
                this.loading = false;
                this.message = "Login failed!";
            } else {
                this.$router.push("/profile");
            }
        },
    },
};
</script>

<style>
@import "../assets/styles/main.css";
.btn-login{
    border-radius: 20px;
    border: 2px solid #080808;
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
.login-title{
    color:   #000000;
    margin-left: 120px;
    font-family: 'Acme';
    margin-bottom: 30px;
}
.card-container{
    
    background-color: '#F8DAD0';
    
}
</style>
