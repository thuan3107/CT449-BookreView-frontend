<template>
  <div class="row">
    <div class="col-md-12">
      <div class="mb-3 input-group">
        <input
          type="text"
          class="form-control"
          placeholder="Search by title..."
          v-model="nameToSearch"
        />
        <div class="input-group-append">
          <button class="btn btn-outline-secondary" type="button" @click="searchName">
            Search
          </button>
        </div>
      </div>
    </div>
    <div class="col-md-12 d-flex" v-for="(book, index) in bookSearch.length > 0 ? bookSearch : book" :key="index">
      <div v-if="currentBookreview && book.bookId === currentBookreview.bookId">
        <BookreviewFullDetails :bookreview="currentBookreview" />
      </div>
      <div v-else class="col-md-8 jumbotron p-4 p-md-5 text-dark rounded bg-light">
        <div class="row overflow-hidden flex-md-row">
          <div class="col d-flex flex-column position-static">
            <p class="d-inline-block mb-2" style="color: #789c73"></p>
          </div>
        </div>
        <div class="col-md-12 px-0 py-3 border-bottom">
          <h1 class="display-4 font-italic text-center" id="title">{{ book.bookName }}</h1>
          <a target="_blank" class="tony-image" :href="book.link"
          input="true"    
            ><img v-bind:src="book.image || this.book.filter(bo => bo.bookId == book.bookId)[0].image" alt="" width="350" height="500"
          /></a>
        </div>
        <div class="border-top p-1">
          
          <h4 class="px-1 py-3 text-center" id="title">
            <q>{{ book.title }}</q>
          </h4>
          <p class="text-justify font-italic text-right" style="font-size: 20px; color: #789c73">
            {{ book.author }}
          </p>
        </div>
      </div>
      <div class="col-md-4">
        <h4 style="color: #10bded; font-family: 'Acme' ">Status</h4>
        <div class="list-group">
          <div
            class="list-group-item"
            :class="{ active: index == currentIndex && currentBookreview.bookId === book.bookId }"
            v-for="(bookreview, index) in book.review"
            :key="bookreview.id"
            @click="setActiveBookreview(bookreview, index)"
          >
            <div class="d-flex w-100 justify-content-between">
              <strong class="mb-1" style="color: #756262">{{ bookreview.title }}</strong>
            </div>
            <p class="mb-1 font-italic text-secondary">{{ bookreview.bookname }}</p>
          </div>
        </div>

        <button class="btn-button" @click="goToAddBookreview(book.bookId)">ADD</button>

        <button class="btn-button" @click="removeAllBookreviews(book.review)">DELETE ALL</button>
      </div>
    </div>
  </div>
</template>

<script>
import BookreviewService from '../services/bookreview.service';
import BookreviewFullDetails from '../components/BookreviewFullDetails';
import tony from '../assets/styles/tony.jpg';
import shortlife from '../assets/styles/shortlife.jpg';
import docvi from '../assets/styles/docvi.jpg';

export default {
  name: 'BookreviewHome',
  components: {
    BookreviewFullDetails,
  },
  data() {
    return {
      bookreviews: [],
      book: [
        {
          bookId: 'book1',
          title:
            'Đọc sách rất quan trọng. Nếu bạn đọc sách đúng cách, cả thế giới sẽ mở ra cho bạn',
          image: tony,
          bookname: 'Cafe sáng cùng Tony',
          author: 'Barack Obama',
          link: 'https://images.thuvienpdf.com/iww1nxvXuD.webp',
          review: [],
        },
        {
          bookId: 'book2',
          title: 'Bạn chọn là một nhà lãnh đạo hay trở thành một người tầm thường?',
          image: shortlife,
          bookname: 'Đời ngắn đừng ngủ dài',
          author: 'Robin Sharma',
          link: 'https://images.thuvienpdf.com/OUB4y1.webp',
          review: [],
        },
        {
          bookId: 'book3',
          title: `Đọc vị bất kì ai - để không bị lừa dối và lợi dụng. <br />
              Bạn băn khoăn không biết người ngồi đối diện đang nghĩ gì? Họ có đang nói dối bạn
              không? Đối tác đang ngồi đối diện với bạn trên bàn đàm phán đang nghĩ gì và nói gì
              tiếp theo?`,
          image: docvi,
          bookname: 'Đọc vị bất kì ai',
          author: 'David J.Lieberman',
          link: 'https://images-na.ssl-images-amazon.com/images/I/51Bb5oTu2+L._SX314_BO1,204,203,200_.jpg',
          review: [],
        },
      ],
      currentBookreview: null,
      currentIndex: -1,
      nameToSearch: '',
      bookSearch: []
    };
  },
  methods: {
    setActiveBookreview(bookreview, index) {
      console.log(bookreview);
      this.currentBookreview = bookreview;
      this.currentIndex = bookreview ? index : -1;
    },

    async retrieveBookreviews() {
      const [error, response] = await this.handle(BookreviewService.getAll());
      if (error) {
        console.log(error);
      } else {
        this.book.forEach((book1) => (book1.review = []));
        response.data.forEach((review) => {
          this.book.forEach((book1) => {
            if (book1.bookId === review.bookId) {
              book1.review.push(review);
            }
          });
        });
        console.log(response.data);
      }
    },

    refreshList() {
      this.retrieveBookreviews();
      this.currentBookreview = null;
      this.currentIndex = -1;
    },
  
    async removeAllBookreviews(id) {
      const list = id.map((id1) => id1.id);
      const [error, response] = await this.handle(BookreviewService.deleteAll(list));
      if (error) {
        console.log(error);
      } else {
        console.log(response.data);
        this.refreshList();
      }
    },
    goToAddBookreview(bookId) {
      this.$router.push(`/addbookreview/${bookId}`);
    },
    async searchName() {
      const [error, response] = await this.handle(BookreviewService.findByName(this.nameToSearch));
      if (error) {
        console.log(error);
      } else {
        this.bookreviews = response.data;
        this.bookSearch= [...response.data];
        this.setActiveBookreview(null);
        console.log(response.data);
      }
    },
  },
  mounted() {
    this.retrieveBookreviews();
  },
};
</script>

<style>
#title {
  font-family: 'Playfair Display';
  color: #756262;
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
.tony-image img {
  margin-left: 25%;
}
</style>
