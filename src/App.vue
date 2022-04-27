<template>
    <div id="app" >
        <div class="container">
            <header class="border-bottom py-3" >
                <div class="row flex-nowrap justify-content-between align-items-center" >
                    <!-- <div class="col-4 pt-1">
                    </div> -->
                    <div class="col-4 text-center">
                        <a class="book-icon" href="/"><img src="@/assets/styles/book.png" alt="" ></a>
                        <a href="/" style="font-family: 'Annie Use Your Telescope'; font-size: 60px; text-decoration: none; color: #21bae3; font-weight: 600; text-align: left; ">
                        ThichreView</a>
                    </div>

                    <div v-if="currentUser" class="col-4 d-flex justify-content-end align-items-centernu">
                        <router-link to="/profile" class="nav-link" style="color: #756262">
                        {{ currentUser.username }}
                        </router-link>
                        <a class="btn-logout" @click.prevent="logout">LOGOUT</a>
                    </div>

                    <div v-if="!currentUser" class="col-4 d-flex justify-content-end align-items-center">
                        <router-link to="/register" class="btn-signup-top"> 
                            Sign Up 
                        </router-link>
                        <a >|</a>
                        <router-link to="/login" class="btn-login-top">
                             Log In
                        </router-link>
                    </div>
                </div>
            </header>

            <div v-if="currentUser" class="border-bottom py-1 mb-2 ">
                <nav class="nav d-flex justify-content-md-center">
                    <li class="p-1">
                        <router-link to="/bookreview" class="nav-link">
                            Home
                        </router-link>
                    </li>

                    <li class="p-1">
                        <router-link to="/author" class="nav-link">
                            Author
                        </router-link>
                    </li>

                    <li class="p-1">
                        <router-link to="/reviewer" class="nav-link" style="">
                            Bookstore
                        </router-link>
                    </li>

                </nav>
            </div>
        </div>

        <div class="container mt-3 mb-5">
            <router-view />
        </div>

        <footer class="mt-5 text-center border-top">
            <a href="#" style="color: #BCFEFE font-family: 'Acme' ">BACK TO TOP</a>
        </footer>
    </div>
</template>


<script>
import { mapGetters, mapMutations } from "vuex";
import "@fontsource/acme" ;
import "@fontsource/annie-use-your-telescope" ;
export default {
    name: 'App',
    computed: {
        ...mapGetters({
        currentUser: "loggedInUser",
    }),
  },
    methods: {
        ...mapMutations([
            "initAuthState"
        ]),

    logout() {
        this.$store.commit("logout");
        this.$router.push("login");
        },
    },
    mounted() {
        this.initAuthState();
        }
    };
</script>

<style>

.nav-link {
    color: #000000;
    font-family: 'Acme';
    font-size: 20px;
}
.nav-link:hover, .nav-link:focus {
    color: #000000;
}
.book-icon img{
    width: 100px;
    position: relative;
    left: 20px;
    
    
}
.btn-signup-top{
    border-color: #10bded;
    font-size: large;
    margin-right: 5px;
    font-family: 'Acme';
}
.btn-login-top{
    border-color: #10bded;
    font-size: large;
    margin-left: 5px;
    font-family: 'Acme';

}
.btn-logout {
    border-color: #10bded;
    font-size: large;
    margin-left: 5px;
    font-family: 'Acme';
}
</style>