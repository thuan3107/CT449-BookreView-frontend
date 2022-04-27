<template>
  <div class="create-form">
    <div>
      <h4 style="color: #10bded; font-family: 'Acme'; text-align: center">ADD STATUS</h4>
      <BookreviewForm :bookreview="bookreview" @bookreview-submit="createBookreview" />
      {{ bookId }}
      <p>{{ message }}</p>
    </div>
  </div>
</template>
<script>
import BookreviewService from '../services/bookreview.service';
import BookreviewForm from '../components/BookreviewForm';
export default {
  name: 'BookreviewCreate',
  components: {
    BookreviewForm,
  },
  data() {
    return {
      bookreview: {},
      message: '',
    };
  },
  methods: {
    async createBookreview(data) {
      data['bookId'] = this.$route.params.id;
      const [error, response] = await this.handle(BookreviewService.create(data));
      if (error) {
        console.log(error);
      } else {
        console.log(response.data);
        this.message = 'The status has been added successfully!';
      }
    },
  },
};
</script>
<style>
.create-form {
  font-family: 'Acme';
  max-width: 750px;
  margin: auto;
}
</style>
