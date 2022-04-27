<template>
    <Form 
        @submit="$emit('reviewer-submit', reviewerLocal)"
        :validation-schema="schema"    
    >
        <div class="form-group">
            <label for="name">Name</label>
            <Field
                name="name"
                type="name"
                class="form-control"
                v-model="reviewerLocal.name"
            />
            <ErrorMessage name="bookname" class="error-feedback" /> 
        </div >
        <div class="form-group">
            <label for="profile" style="color: #5b896b; font-family: 'Acme'">Information</label>
            <Field
                name="profile"
                as="textarea"
                class="form-control"
                v-model="reviewerLocal.profile"
            />
            <ErrorMessage name="profile" class="error-feedback" />
        </div>
        <div class="form-group form-check">
            <input 
                name="favorite"
                type="checkbox"
                class="form-check-input"
                v-model="reviewerLocal.favorite"
            />
            <label for="favorite" class="form-check-label" style="font-family: 'Acme' ">
                <strong>Favorite</strong>
            </label>
        </div>

        <div class="form-group">
            <button class="btn-button-edit">Save</button>
            <button
                v-if="reviewerLocal.id"
                type="button"
                class="btn-button-edit"
                @click="$emit('reviewer-delete', reviewerLocal.id)"
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
    name: "AuthorForm",
    components: {
        Form,
        Field,
        ErrorMessage,
    },
    emits: ["reviewer-submit", "reviewer-delete"],
    props: ["reviewer"],
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
            reviewerLocal: this.reviewer,
            schema,
        };
    },
};
</script>

<style>
    @import "../assets/styles/main.css";    
</style>