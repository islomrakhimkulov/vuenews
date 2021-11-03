<template>
    <div class="sourceselection">
        <div>
            <div class="jumbotron shadow-sm">
                <h2 class="text-center">News List</h2>
                <h4>Select News Source</h4>

                <select class="form-control" v-on:change="sourceChanged">
                    <option value="" disabled>Please select news source ...</option>
                    <option v-bind:value="source.id" v-for="source in sources" :key="source.id">{{ source.name }}</option>
                </select>

                <div v-if="sources">
                    <h6 class="py-2">{{ source.description }}</h6>
                    <a v-bind:href="source.url" class="btn link-btn shadow-sm" target="_blank">Go To {{ source.name }} Website</a>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'sourceselection',
    data () {
        return {
           sources: [],
           source: ''
        }
    },
    methods: {
        sourceChanged (e) {
            for (var i=0; i<this.sources.length; i++) {
                if (this.sources[i].id == e.target.value) {
                    this.source = this.sources[i];
                }
            }
            this.$emit('sourceChanged', e.target.value);
        }
    },
    created: function () {
        this.$http.get('https://newsapi.org/v1/sources?language=en')
         .then(response => {
            //  success callback
            this.sources  = response.data.sources;
           
            this.sources.forEach( (item, index, arr) => {
                console.log(item);
            });
         }, response => {
            //  err call back
         });
    },
    
}
</script>

<style scoped>
.link-btn {
    background-color: #42B983;
    color: #fff;
}
</style>