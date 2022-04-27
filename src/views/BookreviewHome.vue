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
    <div class="col-md-8">
      <div v-if="currentBookreview">
        <BookreviewFullDetails :bookreview="currentBookreview" />
      </div>
      <div v-else class="jumbotron p-4 p-md-5 text-dark rounded bg-light">
        <div class="col-md-12">
          <div class="row overflow-hidden flex-md-row">
            <div class="col d-flex flex-column position-static">
              <p class="d-inline-block mb-2" style="color: #789c73"></p>
            </div>
          </div>
        </div>
        <div class="col-md-12 px-0 py-3 border-bottom">
          <h1 class="display-4 font-italic text-center" id="title"> </h1>
          <a class="tony-image" href="https://reviewsach.net/ca-phe-cung-tony-buoi-sang/"
            ><img src="../assets/styles/tony.jpg" alt="" width="350" height="500" 
          /></a>
        </div>
        <div class="border-top p-1">
          <h4 class="px-1 py-3 text-center" id="title">
            <q>Đọc sách rất quan trọng. Nếu bạn đọc sách đúng cách, cả thế giới sẽ mở ra cho bạn</q>
          </h4>
          <p class="text-justify font-italic text-right" style="font-size: 20px; color: #789c73">
            Barack Obama
          </p>
        </div>
      </div>
    </div>
    <div class="col-md-4">
      <h4 style="color: #756262; font-family: 'Acme'">Status</h4>
      <div class="list-group">
        <div
          class="list-group-item"
          :class="{ active: index == currentIndex }"
          v-for="(bookreview, index) in bookreviews"
          :key="bookreview.id"
          @click="setActiveBookreview(bookreview, index)"
        >
          <div class="d-flex w-100 justify-content-between">
            <strong class="mb-1" style="color: #756262">{{ bookreview.title }}</strong>
          </div>
          <p class="mb-1 font-italic text-secondary">{{ bookreview.bookname }}</p>
        </div>
      </div>

      <button class="btn-button" @click="goToAddBookreview">ADD</button>

      <button class="btn-button" @click="removeAllBookreviews">DELETE ALL</button>
    </div>

    <div class="col-md-8">
      <div v-if="currentBookreview">
        <BookreviewFullDetails :bookreview="currentBookreview" />
      </div>
      <div v-else class="jumbotron p-4 p-md-5 text-dark rounded bg-light">
        <div class="col-md-12">
          <div class="row overflow-hidden flex-md-row">
            <div class="col d-flex flex-column position-static">
              <p class="d-inline-block mb-2" style="color: #789c73"></p>
            </div>
          </div>
        </div>
        <div class="col-md-12 px-0 py-3 border-bottom">
          <h1 class="display-4 font-italic text-center" id="title"></h1>
          <a
            class="tony-image"
            href="https://kesachonline.com/review-sach-doi-ngan-dung-ngu-dai-la-lanh-dao-hay-nguoi-tam-thuong.html"
            ><img src="../assets/styles/shortlife.jpg" alt="" width="350" height="500"
          /></a>
        </div>
        <div class="border-top p-1">
          <h4 class="px-1 py-3 text-center" id="title">
            <q>Bạn chọn là một nhà lãnh đạo hay trở thành một người tầm thường?</q>
          </h4>
          <p class="text-justify font-italic text-right" style="font-size: 20px; color: #789c73">
            Robin Sharma
          </p>
        </div>
      </div>
    </div>
    <div class="col-md-4">
      <h4 style="color: #10bded; font-family: 'Acme'; ">Status</h4>
      <div class="list-group">
        <div
          class="list-group-item"
          :class="{ active: index == currentIndex }"
          v-for="(bookreview, index) in bookreviews"
          :key="bookreview.id"
          @click="setActiveBookreview(bookreview, index)"
        >
          <div class="d-flex w-100 justify-content-between">
            <strong class="mb-1" style="color: #756262">{{ bookreview.title }}1</strong>
          </div>
          <p class="mb-1 font-italic text-secondary">{{ bookreview.bookname }}</p>
        </div>
      </div>

      <button class="btn-button" @click="goToAddBookreview">ADD</button>

      <button class="btn-button" @click="removeAllBookreviews">DELETE ALL</button>
    </div>

    <div class="col-md-8">
      <div v-if="currentBookreview">
        <BookreviewFullDetails :bookreview="currentBookreview" />
      </div>
      <div v-else class="jumbotron p-4 p-md-5 text-dark rounded bg-light">
        <div class="col-md-12">
          <div class="row overflow-hidden flex-md-row">
            <div class="col d-flex flex-column position-static">
              <p class="d-inline-block mb-2" style="color: #789c73"></p>
            </div>
          </div>
        </div>
        <div class="col-md-12 px-0 py-3 border-bottom">
          <h1 class="display-4 font-italic text-center" id="title"></h1>
          <a class="tony-image" href="https://revisach.com/doc-vi-bat-ky-ai/"
            ><img src="../assets/styles/docvi.jpg" alt="" width="350" height="500"
          /></a>
        </div>
        <div class="border-top p-1">
          <h4 class="px-1 py-3 text-center" id="title">
            <q
              >Đọc vị bất kì ai - để không bị lừa dối và lợi dụng. <br />
              Bạn băn khoăn không biết người ngồi đối diện đang nghĩ gì? Họ có đang nói dối bạn
              không? Đối tác đang ngồi đối diện với bạn trên bàn đàm phán đang nghĩ gì và nói gì
              tiếp theo?</q
            >
          </h4>
          <p class="text-justify font-italic text-right" style="font-size: 20px; color: #789c73">
            David J.Lieberman
          </p>
        </div>
      </div>
    </div>
    <div class="col-md-4">
      <h4 style="color: #10bded">Status</h4>
      <div class="list-group">
        <div
          class="list-group-item"
          :class="{ active: index == currentIndex }"
          v-for="(bookreview, index) in bookreviews"
          :key="bookreview.id"
          @click="setActiveBookreview(bookreview, index)"
        >
          <div class="d-flex w-100 justify-content-between">
            <strong class="mb-1" style="color: #756262">{{ bookreview.title }}</strong>
          </div>
          <p class="mb-1 font-italic text-secondary">{{ bookreview.bookname }}</p>
        </div>
      </div>

      <button class="btn-button" @click="goToAddBookreview">ADD</button>

      <button class="btn-button" @click="removeAllBookreviews">DELETE ALL</button>
    </div>
  </div>
</template>

<script>
import BookreviewService from '../services/bookreview.service';
import BookreviewFullDetails from '../components/BookreviewFullDetails';

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
          image: '../assets/styles/tony.jpg',
          bookname: 'Cafe sáng cùng Tony',
          author: 'Barack Obama',
          link: 'https://reviewsach.net/ca-phe-cung-tony-buoi-sang/',
          review: [],
        },
        {
          bookId: 'book2',
          title: 'Bạn chọn là một nhà lãnh đạo hay trở thành một người tầm thường?',
          image: '../assets/styles/shortlife.jpg',
          bookname: 'Đời ngắn đừng ngủ dài',
          author: 'Robin Sharma',
          link: 'https://kesachonline.com/review-sach-doi-ngan-dung-ngu-dai-la-lanh-dao-hay-nguoi-tam-thuong.html',
          review: [],
        },
        {
          bookId: 'book3',
          title: `Đọc vị bất kì ai - để không bị lừa dối và lợi dụng. <br />
              Bạn băn khoăn không biết người ngồi đối diện đang nghĩ gì? Họ có đang nói dối bạn
              không? Đối tác đang ngồi đối diện với bạn trên bàn đàm phán đang nghĩ gì và nói gì
              tiếp theo?`,
          image: '../assets/styles/docvi.jpg',
          bookname: 'Đọc vị bất kì ai',
          author: 'David J.Lieberman',
          link: 'https://revisach.com/doc-vi-bat-ky-ai/',
          review: [],
        },
      ],
      currentBookreview: null,
      currentIndex: -1,
      nameToSearch: '',
    };
  },
  methods: {
    setActiveBookreview(bookreview, index) {
      this.currentBookreview = bookreview;
      this.currentIndex = bookreview ? index : -1;
    },

    async retrieveBookreviews() {
      const [error, response] = await this.handle(BookreviewService.getAll());
      if (error) {
        console.log(error);
      } else {
        this.bookreviews = response.data;
        console.log(response.data);
      }
    },

    refreshList() {
      this.retriveBookreviews();
      this.currentBookreview = null;
      this.currentIndex = -1;
    },

    async removeAllBookreviews() {
      const [error, response] = await this.handle(BookreviewService.deleteAll());
      if (error) {
        console.log(error);
      } else {
        console.log(response.data);
        this.refreshList();
      }
    },
    goToAddBookreview() {
      this.$router.push('/addbookreview');
    },
    async searchName() {
      const [error, response] = await this.handle(BookreviewService.findByName(this.nameToSearch));
      if (error) {
        console.log(error);
      } else {
        this.bookreviews = response.data;
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
  font-family: 'Acme';
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
