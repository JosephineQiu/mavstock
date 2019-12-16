<template>
    <v-app>
        <div>
            <md-layout v-for="publish in publishers" :key="publish.id" md-flex="33" md-align="center">
                <md-card md-with-hover class="card">
                    <md-card-header>
                        <div class="md-title">{{publish.name}}</div>
                    </md-card-header>

                    <md-card-content>
                        {{publish.description}}
                    </md-card-content>

                    <md-card-actions>
                        <md-button @click="readMore(publish)">About this publisher</md-button>
                        <md-button @click="getFeed(publish)">Get News From</md-button>
                    </md-card-actions>
                </md-card>
            </md-layout>
        </div>
    </v-app>
</template>

<script>
    export default {
        name: "Publisher",

    data() {
      return {
        publishers: '',
      }
    },

    methods: {
      initData: function() {
        this
          .$http
          .get('https://newsapi.org/v1/sources?language=en')
          .then(response => (this.publishers = response.body.sources))
          .catch(function(err){
            this.publishers = err;
          })
      },
      readMore: function(publish){
        window.open(publish.url, '_blank');
      },
      getFeed: function (publish) {
        this.$router.push({name:'News', params: {id: publish.id}})
      }
    },
    created: function(){
      this.initData();
    }
    }
</script>

<style scoped>

</style>