<template>
    <Form 
        @submit="$emit('bookreview-submit', bookreviewLocal)"
        :validation-schema="schema"    
    >
        <div class="form-group">
            <label for="title">Title</label>
            <Field
                name="title"
                type="text"
                class="form-control"
                v-model="bookreviewLocal.title"
            />
            <ErrorMessage name="title" class="error-feedback" />
        </div>
        <div class="form-group">
            <label for="bookname">Book title</label>
            <Field
                name="bookname"
                type="bookname"
                class="form-control"
                v-model="bookreviewLocal.bookname"
            />
            <ErrorMessage name="bookname" class="error-feedback" /> 
        </div>
        <div class="form-group">
            <label for="author">Author</label>
            <Field
                name="author"
                type="text"
                class="form-control"
                v-model="bookreviewLocal.author"
            />
            <ErrorMessage name="author" class="error-feedback" />
        </div>
        <div class="form-group">
            <label for="reviewer">Reviewer</label>
            <Field
                name="reviewer"
                type="text"
                class="form-control"
                v-model="bookreviewLocal.reviewer"
            />
            <ErrorMessage name="reviewer" class="error-feedback" />
        </div >
        <div class="form-group">
            <label for="intro">Introduce</label>
            <Field
                name="intro"
                as="textarea"
                class="form-control"
                v-model="bookreviewLocal.intro" 
            />
            <ErrorMessage name="intro" class="error-feedback" />
        </div>
        <div class="form-group">
            <label for="content">Describe</label>
            <Field
                name="content"
                as="textarea"
                class="form-control"
                v-model="bookreviewLocal.content" 
            />
            <ErrorMessage name="content" class="error-feedback" />
        </div>
        <div class="form-group form-check check">
            <input 
                name="favorite"
                type="checkbox"
                class="form-check-input"
                v-model="bookreviewLocal.favorite"
            />
            <label for="favorite" class="form-check-label" style=" font-family: 'Acme'">
                <p>Favorite</p>
            </label>
        </div>

        <div class="form-group">
            <button class="btn-button-edit">SAVE</button>
            <button
                v-if="bookreviewLocal.id"
                type="button"
                class="btn-button-edit"
                @click="$emit('bookreview-delete', bookreviewLocal.id)"
            >
                Delete
            </button>
        </div>

    </form>
</template>

<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage} from "vee-validate";
import "@fontsource/acme" ;


export default {
    name: "BookreviewForm",
    components: {
        Form,
        Field,
        ErrorMessage,
    },
    emits: ["bookreview-submit", "bookreview-delete"],
    props: ["bookreview"],
    data() {
        const schema = yup.object().shape({
            title: yup
                .string()
                .required("The title must be valid.")
                .min(2, "Title has at least 2 characters.")
                .max(100, "Titles with at most 100 characters."),
            bookname: yup
                .string()
                .required("The title of the book must be valid.")
                .min(2, "Book title must have at least 2 characters.")
                .max(100, "Book title has at most 100 characters."),
            author: yup
                .string()
                .required("Author name must be valid.")
                .min(2, "Author name must have at least 2 characters.")
                .max(50, "Author name can be up to 50 characters."),
            reviewer: yup
                .string()
                .required("The reviewer name must be valid.")
                .min(2, "Reviewer name must be at least 2 characters.")
                .max(50, "Reviewer's name has a maximum of 50 characters."), 
            intro: yup
                .string()
                .required("The introduce must be valuable.")
                .min(50, "The introduce must be at least 50 characters.")
                .max(2000, "The introduce can be up to 2000 characters."),    
            content: yup
                .string()
                .required("Reviews must be valuable.")
                .min(50, "Reviews must be at least 50 characters long.")
                .max(2000, "Review content with at most 2000 characters."),          
        });
        return {
            bookreviewLocal: this.bookreview,
            schema,
        };
    },
};
</script>

<style>
    @import "../assets/styles/main.css";    
</style>