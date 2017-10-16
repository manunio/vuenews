<template>
  <div class="newslist">
    <!-- NewsList -->
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <ul class="media-list">
            <li  v-for="article in articles">
              <div class="media">
                <div class="media-left media-middle">
                  <a v-bind:href="article.url">
				      <img class="media-object" v-bind:src="article.urlToImage" alt="Vue News Image ">
				</a>
                </div>
                <div class="media-body">
                  <h4 class="media-heading"><a v-bind:href="article.url" target="_blank">{{ article.title }} </a></h4>
                  <h5><i>by: {{ article.author }}</i></h5>
                  <p>{{article.description}}</p>

                </div>
              </div>
            </li>
            <!-- <li class="media" v-for="article in articles">
              <div class="media-left">
                <a v-bind:href="article.url"><img v-bind:src="article.urlToImage" alt=""></a>
              </div>
              <div class="media-body">
                <h4 class="media-heading">
					<a v-bind:href="article.url" target="_blank">{{ article.title }} </a>
					</h4>
                <h5><i>by {{ article.author }}</i></h5>
                <p>{{article.description}}</p>
              </div>
            </li> -->
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'newslist',
  props: ['source'],
  data() {
    return {
      articles: []
    }
  },
  methods: {
    updateSource: function(source) {
     
      this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=f71da1a174af443c9912c0bbe06b1f4d')
        .then(response => {
          this.articles = response.data.articles;
        });

    }
  },
  created: function() {
    this.updateSource(this.source);
  },
  watch: {
    source: function(val) {
      this.updateSource(val);
    }
  }

}

</script>
<style scoped>
.media-object {
  width: 128px;
  padding: 10px;
}

.media {
  border-top: 1px solid lightgray;
  padding-top: 20px;
}

</style>
