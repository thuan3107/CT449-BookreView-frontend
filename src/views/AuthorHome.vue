<template>
    <div class="list row">
        <div class="col-md-12">
            <div class="mb-3 input-group">
                <input 
                    type="text"
                    class="form-control"
                    placeholder="Search by name..."
                    v-model="nameToSearch"/>
                <div class="input-group-append">
                    <button 
                        class="btn btn-outline-secondary"
                        type="button"
                        @click="searchName"
                    >
                        Search
                    </button>
                </div>
            </div>
        </div>

        <div class="col-md-4">
            <h4 style="color: #10bded; font-family: 'Acme'">Author</h4>
            <ul class="list-group">
                <li
                    class="list-group-item"
                    :class="{ active: index == currentIndex }"
                    v-for="(author, index) in authors"
                    :key="author.id"
                    @click="setActiveAuthor(author, index)"    
                >
                    <span style="color: #756262">{{ author.name }}</span>
                </li>
            </ul>

            <button class="btn-button" @click="goToAddAuthor">
                ADD
            </button>

            <button class="btn-button" @click="removeAllAuthors">
                DELETE ALL
            </button>
        </div>
        <div class="col-md-8">
            <div v-if="currentAuthor">
                <AuthorDetails 
                    :author="currentAuthor"
                />
            </div>
        </div>
    </div>
</template>

<script>
import AuthorDetails from "../components/AuthorDetails";
import AuthorService from "../services/author.service";


export default {
    name: "AuthorHome",
    components: {
        AuthorDetails,
    },
    data() {
        return {
            authors: [],
            currentAuthor: null,
            currentIndex: -1,
            nameToSearch: "",
        };
    },
    methods: {
        setActiveAuthor(author, index) {
            this.currentAuthor = author;
            this.currentIndex = author ? index : -1;
        },

        async retrieveAuthors() {
            const [error, response] = await this.handle(
                AuthorService.getAll()
            );
            if (error) {
                console.log(error);
            } else {
                this.authors = response.data;
                console.log(response.data);
            }
        },
        
        refreshList() {
            this.retriveAuthors();
            this.currentAuthor = null;
            this.currentIndex = -1;
        },

        async removeAllAuthors() {
            const [error, response] = await this.handle(
                AuthorService.deleteAll()
            );
            if (error){
                console.log(error);
            } else {
                console.log(response.data);
                this.refreshList();
            }
        },
        goToAddAuthor() {
            this.$router.push("/addauthor");
        },
        async searchName() {
            const [error, response] = await this.handle(
                AuthorService.findByName(this.nameToSearch)
            );
            if(error){
                console.log(error);
            } else {
                this.authors = response.data;
                this.setActiveAuthor(null);
                console.log(response.data);
            }
        },
        
    }, 
    mounted() {
        this.retrieveAuthors();
    },   
};
</script>

<style>
.list {
    text-align: left;
    max-width: 900px;
    margin: auto;
}
.list-group-item.active {
  z-index: 2;
  color: #fff;
  background-color: #76575727;
  border-color: #968080ab;
}
.list-group-item:hover {
  color: #fff;
  background-color: #76575727;
}
.btn:hover {
    color: #756262;
    background-color: #76575727;
    border-color: #968080ab;
}
.form-control:focus {
  color: #495057;
  background-color: #fff;
  border-color: #968080ab;
  outline: 0;
  box-shadow: 0 0 0 0.2rem rgba(94, 74, 44, 0.315);
}

.btn-button {
    border-radius: 30px;
    border: 2px solid #080808;
    background-color: #eaea70;
    color: #000000;
    font-size: 18px;
    font-weight: bold;
    text-transform: uppercase;
    transition: transform 50ms ease-in;
    margin-top: 25px;
    margin-left: 5px;
    font-family: 'Acme';
}

</style>