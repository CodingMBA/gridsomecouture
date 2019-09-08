<template>
  <Layout>
    <h1># {{ $page.tag.title }}</h1>
    <article
      v-for="edge in $page.tag.belongsTo.edges"
      :key="edge.node.id"
      style="margin-bottom: 2em;"
    >
      <g-image :src="edge.node.cover_image" width="100%" />
      <h2>{{ edge.node.title }}</h2>
      <p>{{ edge.node.excerpt }}</p>
      <p>Posted {{ edge.node.date }} - {{ edge.node.timeToRead }} min read</p>
      <div>
        <g-link
          v-for="tag in edge.node.tags"
          :key="tag.id"
          :to="tag.path"
          style="padding-right: .25em"
          >#{{ tag.id }}</g-link
        >
      </div>
      <g-link :to="edge.node.path">Read Post</g-link>
    </article>
  </Layout>
</template>

<page-query>
query ($id: String!) {
  tag (id: $id) {
    title
    belongsTo {
      edges {
        node {
          ... on Post {
            id
            title
            excerpt
            date (format: "MMMM Do, YYYY")
            tags {
              id
              path
            }
            timeToRead
            path
            cover_image (width: 1000, height: 300, blur: 10)
          }
        }
      }
    }
  }
}
</page-query>

<script>
export default {};
</script>

<style></style>
