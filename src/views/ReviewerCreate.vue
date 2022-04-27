<template>
    <div class="create-form" >
        <div>
        <h4 style="color: #10bded; font-family: 'Acme'; text-align: center ">Add titles to the bookshelf</h4>
        
        <ReviewerForm
            :reviewer="reviewer"
            @reviewer-submit="createReviewer"
        />
        <p>{{ message }}</p>
        </div>
    </div>
</template>
<script>
import ReviewerService from "../services/reviewer.service";
import ReviewerForm from "../components/ReviewerForm";
export default {
    name: "ReviewerCreate",
    components: {
        ReviewerForm,
    },
    data() {
        return {
            reviewer: {},
            message: "",
        };
    },
    methods: {
        async createReviewer(data) {
            const [error, response] = await this.handle(
                ReviewerService.create(data)
            );
            if (error) {
                console.log(error);
            } else {
                console.log(response.data);
                this.message = "Book title has been added successfully!";
            }
        },
        },
    };
</script>
<style>
.create-form {
    max-width: 400px;
    margin: auto;
}

</style>