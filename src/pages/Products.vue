<template>
  <Layout>
    <h1>Products</h1>
    <div
      v-for="edge in $page.allContentfulProduct.edges"
      :key="edge.node.id"
      style="text-align: center;"
    >
      <h2 style="margin-bottom: 0.25em;">{{ edge.node.name }}</h2>
      <button
        class="snipcart-add-item cart-button"
        :data-item-id="edge.node.id"
        :data-item-name="edge.node.name"
        :data-item-image="edge.node.image.file.url"
        :data-item-price="edge.node.price"
        :data-item-url="edge.node.path"
      >
        Buy for ${{ edge.node.price }}
      </button>
      <g-image
        :src="edge.node.image.file.url"
        style="width: 100%; height: 300px; object-fit: contain;"
        :alt="edge.node.image.title"
      ></g-image>
      <p>{{ edge.node.description }}</p>
    </div>
    <Pager :info="$page.allContentfulProduct.pageInfo" link-class="pager" />
  </Layout>
</template>

<page-query>
query ($page: Int) {
  allContentfulProduct (perPage: 2, page: $page) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        id
        path
        name
        price
        description
        image {
          title
          file {
            url
          }
        }
      }
    }
  }
}
</page-query>

<script>
import { Pager } from "gridsome";

export default {
  components: { Pager },
  metaInfo: {
    title: "Products",
    meta: [
      { charset: "utf-8" },
      { name: "author", content: "Bodhi Code" },
      {
        name: "description",
        content:
          "Discover our entire range of luxury apparel, shoes, and accessories"
      },
      {
        name: "keywords",
        content: "Premium Jackets, High-End Clothing, Designer Sunglasses"
      }
    ]
  }
};
</script>

<style>
.pager {
  font-size: 1rem;
  letter-spacing: 0.5px;
  padding: 40px 15px;
}

.cart-button {
  background-color: forestgreen;
  border: none;
  border-radius: 5px;
  color: white;
  padding: 8px 16px;
  margin-bottom: 10px;
  text-decoration: none;
  font-size: 1rem;
}
</style>
