<template>
    <div class="jumbotron p-4 p-md-5 text-dark rounded bg-light">
        <div class="col-md-12">
                <div class="row overflow-hidden flex-md-row">
                    <div class="col d-flex flex-column position-static">
                        <p 
                            class="d-inline-block mb-2" 
                            style="color: #000000" >
                            Đánh giá bởi {{ bookreview.reviewer }}
                        </p>
                    </div>
                </div>
        </div>
        <div class="col-md-12 px-0 py-3 border-bottom">
          <h1 class="display-4 font-italic text-center" id="title">{{ bookreview.title }}</h1>
        </div>

        <div class="border-top p-1">
            <h2 class="px-1 py-3 font-weight-bold text-center" id="title"> {{ bookreview.bookname }}</h2>
            <p class="font-italic text-right" style="font-size: 20px; color: #5b896b; font-family: 'Acme'">{{ bookreview.author }}</p>
        </div>

        <div class="col-md-12 p-3">
          <h5 class="font-weight-bold"  style="color: #5b896b; font-family: 'Acme'">Introduce</h5>
          <p class="text-justify">{{ bookreview.intro }}</p>
          <h5 class="font-weight-bold"  style="color: #5b896b; font-family: 'Acme'">Describe</h5>
          <p class="text-justify">{{ bookreview.content }}</p>
        </div>
        
        <div class="row mb-2">
            <div class="col-md-6">
                    <div class="col p-3 d-flex flex-column position-static">
                        <strong class="d-inline-block" style="color: #5b896b; font-family: 'Acme' ">
                            Favorite:
                            <i v-if="bookreview.favorite" style="color: red" class="fas fa-heart"></i>
                            <i v-else class="far fa-heart"></i>
                        </strong>
                    </div>
            </div>
            <div class="col-md-6">
                    <div class="col p-3 d-flex flex-column position-static">
                        <strong class="d-inline-block text-right" >
                            <router-link style="color: #5b896b; font-family: 'Acme'" :to="'/editbookreview/' + bookreview.id">
                                <span >Edit <i class="far fa-edit"></i></span>
                            </router-link>
                        </strong>
                    </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "BookreviewFullDetails",
    props: ["bookreview"],
    
};
</script>

<style>
#title {
    font-family: "Playfair Display";
    color: #756262;
}

</style>
