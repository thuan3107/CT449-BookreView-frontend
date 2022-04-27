<template>
    <Form 
        @submit="$emit('author-submit', authorLocal)"
        :validation-schema="schema"    
    >
        <div class="form-group">
            <label for="name">Name</label>
            <Field
                name="name"
                type="name"
                class="form-control"
                v-model="authorLocal.name"
            />
            <ErrorMessage name="name" class="error-feedback" /> 
        </div >
        <div class="form-group">
            <label for="profile" style="color= #5b896b; font-family: 'Acme' ">Information</label>
            <Field
                name="profile"
                as="textarea"
                class="form-control"
                v-model="authorLocal.profile"
            />
            <ErrorMessage name="profile" class="error-feedback" />
        </div>
        <div class="form-group form-check">
            <input 
                name="favorite"
                type="checkbox"
                class="form-check-input"
                v-model="authorLocal.favorite"
            />
            <label for="favorite" class="form-check-label">
                <strong style="font-family: 'Acme'  ">Favorite</strong>
            </label>
        </div>

        <div class="form-group">
            <button class="btn-button-edit">Save</button>
            <button
                v-if="authorLocal.id"
                type="button"
                class="btn-button-edit"
                @click="$emit('author-delete', authorLocal.id)"
            >
                Delete
            </button>
        </div>

    </form>
</template>
<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage} from "vee-validate";

export default {
    name: "AuthorForm",
    components: {
        Form,
        Field,
        ErrorMessage,
    },
    emits: ["author-submit", "author-delete"],
    props: ["author"],
    data() {
        const schema = yup.object().shape({
            name: yup
                .string()
                .required("The name must have a value.")
                .min(2, "The name must be at least 2 characters.")
                .max(50, "The name has at most 50 characters."),
            profile: yup
                .string(),           
        });
        return {
            authorLocal: this.author,
            schema,
        };
    },
};
</script>

<style>
    @import "../assets/styles/main.css";
    
</style>