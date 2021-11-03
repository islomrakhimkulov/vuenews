<template>
    <div class="newsList">
        <div class="container">
            <ul class="media-list">
                <li class="media" v-for="article in articles" :key="article">
                    <div class="row">
                        <div class="col-md-4 py-1 media-left">
                            <a v-bind:href="article.url" target="_blank">
                                <img class="rounded-top img-fluid media-object" v-bind:src="article.urlToImage" alt="">
                            </a>
                        </div>
                        <div class="col-md-8 py-1 media-body">
                            <h4 class="media-heading">
                                <a class="article-title" v-bind:href="article.url" target="_blank">{{ article.title }}</a>
                            </h4>
                            <h5><i>by {{ article.author }} </i></h5>
                            <p>{{ article.description }}</p>
                        </div>
                    </div>
                </li>
            </ul>
        </div>
        <footer class="text-center">
            <p>News</p>
        </footer>
    </div>
</template>

<script>

export default {
    name: 'newslist',
    props: ['source'],
    data () {
        return {
            articles: [],
        }
    },
    methods: {
        updateSource(source){
            this.$http.get('https://newsapi.org/v1/articles?source=' + source + '&apiKey=8dd797530e924c0184657317575e4430')
             .then(response => {
                 this.articles = response.data.articles;
             });
        }
    },
    created() {
        this.updateSource(this.source);
    },
    watch: {
        source(val) {
            this.updateSource(val);
        }
    }
}
</script>

<style scoped>
ul {
    padding-inline-start: 0px;
}
.article-title{
    color: #42B983;
}
footer{
    padding: 17px 0 5px 0;
    background-color: #42B983;
    color: #fff;
}
</style>