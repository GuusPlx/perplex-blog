<template>
  <div class="container mx-auto" v-if="articles && articles.data[0]">
    <nuxt-link to="/">Home</nuxt-link>
    <h1 class="text-8xl font-bold my-10">
      {{ articles.data[0].attributes.title }}
    </h1>
    <div>
      <ul>
        <li>{{ articles.data[0].attributes.publishedAt }}</li>
        <li>{{ articles.data[0].attributes.description }}</li>
        <li>{{ articles.data[0].attributes.author.data.attributes.name }}</li>
      </ul>
      <img
        v-if="articles.data[0].attributes.image.data.attributes.url"
        class="w-80"
        :src="articles.data[0].attributes.image.data.attributes.url"
        alt=""
      />
      <div>
        {{ articles.data[0].attributes.content }}
      </div>
    </div>
  </div>
  <div v-else></div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'CharacterCard',
  apollo: {
    // Dynamic querying
    articles: {
      query: gql`
        query getArticle($slug: String!) {
          articles(filters: { slug: { eq: $slug } }) {
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
          slug: this.$route.params.slug || 'the-internet-s-own-boy',
        }
      },
    },
  },
}
</script>
