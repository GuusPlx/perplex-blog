<template>
  <div class="container mx-auto" v-if="article">
    <nuxt-link to="/">Home</nuxt-link>
    <h1 class="text-8xl font-bold my-10">{{article.data.attributes.title}}</h1>
    <div>
      <ul>
        <li>{{article.data.attributes.publishedAt}}</li>
        <li>{{article.data.attributes.description}}</li>
        <li>{{article.data.attributes.author.data.attributes.name}}</li>
      </ul>
      <img v-if="article.data.attributes.image.data.attributes.url" class="w-80" :src="article.data.attributes.image.data.attributes.url" alt="">
      <div>
        {{ article.data.attributes.content }}
      </div>
    </div>
  </div>
  <div v-else>
    
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'CharacterCard',
  apollo: {
    // Dynamic querying
    article: {
      query: gql`
        query getArticle($id: ID!) {
          article(id: $id) {
            data {
              attributes {
                title
                description
                content
                publishedAt
                image {
                  data {
                    attributes {
                      url
                    }
                  }
                }
                author {
                  data {
                    attributes {
                      name
                      picture {
                        data {
                          attributes {
                            url
                          }
                        }
                      }
                    }
                  }
                }
              }
            }
          }
        }
      `,
      variables() {
        return {
          // if the route.params.id is null make id = 1
          id: this.$route.params.id || '1',
        }
      },
    },
  },
}
</script>
