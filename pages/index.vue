<template>
  <div>
    <div class="container mx-auto my-10">
      <h1 class="text-4xl font-bold mb-10 text-pink-500">Perplex <span class="text-gray-800">blog</span></h1> 
      <ul v-if="articles" class="grid grid-cols-3 gap-10" >
        <li v-for="article in articles.data" class="p-10 rounded-xl shadow-lg flex flex-col gap-5">
          <h2 class="text-3xl mb-2">
            {{article.attributes.title}}
          </h2>
          <img class="object-cover w-full h-64 rounded-xl" :src="article.attributes.image.data.attributes.url" alt="">
          <nuxt-link :to="article.attributes.slug">View article</nuxt-link>
        </li>        
      </ul>
    </div>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'IndexPage',

  apollo: {
    articles: gql`
      query getArticles {
        articles {
          data {
            id
            attributes {
              slug
              title
              category {
                data {
                  attributes {
                    name
                  }
                }
              }
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
  },
}
</script>
