<template>
  <Layout>
    <!-- Page Header -->
    <header class="masthead" :style="{
backgroundImage: `url('http://localhost:1337${$page.general.edges[0].node.cover.url}')`
    }">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="site-heading">
              <h1>{{$page.general.edges[0].node.title}}</h1>
              <span class="subheading">{{$page.general.edges[0].node.subTitle}}</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content -->
    <div class="container">
      <div class="row">
        <div class="col-lg-8 col-md-10 mx-auto">
          <div
            class="post-preview"
            v-for="edge in $page.posts.edges"
            :key="edge.node.id"
          >
            <g-link :to="'/post/' + edge.node.id">
              <h2 class="post-title">
                {{ edge.node.title }}
              </h2>
              <!-- <h3 class="post-subtitle">
                Problems look mighty small from 150 miles up
              </h3> -->
            </g-link>
            <p class="post-meta">
              Posted by
              <a href="#">{{ edge.node.createdUserName }}</a>
              {{ edge.node.created_at }}
            </p>
            <p>
              <g-link
                :to="'/tag/' + tag.id"
                v-for="(tag, tagIndex) in edge.node.tags"
                :key="tagIndex"
                >{{ tag.title }}</g-link
              >
            </p>
            <hr />
          </div>

          <!-- Pager -->
          <pager :info="$page.posts.pageInfo" />
        </div>
      </div>
    </div>
  </Layout>
</template> 
<page-query>
query ($page: Int){
 posts: allStrapiPost (perPage: 2, page:$page) @paginate{
    pageInfo {
      totalPages
      currentPage
    }
    edges{
      node{
        id
        title
        createdUserName
        content
        created_at
        cover{
          url
        }
        tags{
          id
          title
        }
      }
    }
  },
   general: allStrapiGeneral{
  edges{
    node{
      title
      subTitle
      cover{
        url
      }
    }
  }
  }
}
</page-query>
<script>
import { Pager } from "gridsome";
export default {
  metaInfo: {
    title: "Hello, world!",
  },
  components: {
    Pager,
  },
};
</script>

<style>
</style>
