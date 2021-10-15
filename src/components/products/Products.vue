<template>
  <section class="container mb-5">
    <h2>Второе задание + дополнительное</h2>

    <div class="product-cards">
      <ProductCard
        v-for="(product, index) of productsItems"
        :key="index"
        :product="product"
      />
    </div>
  </section>
</template>

<script>
import ProductCard from "./ProductCard.vue";
import axios from "axios";

/**
 * Метод для получение товаров из категории
 * @todo Реализовать получение товаров
 * @param {string | number} category id/slug категории
 */

/**
 * Объект продукта
 * @typedef Product
 * @property {number} id айди
 * @property {string} title заголовок
 * @property {string} [image] ссылка на картинку
 * @property {Array <Object>} [colors] возможные цвета
 */

export default {
  components: { ProductCard },
  data() {
    return {
      products: null
    };
  },
  computed: {
    /**
     * @returns {Array <Product> | null}
     */
    productsItems() {
      return this.products;
    }
  },
  methods: {
    getProducts(id) {
      axios
        .get("https://vue-study.skillbox.cc/api/products", {
          params: {
            categoryId: id
          }
        })
        .then(response => (this.products = response.data.items))
        .catch(err => alert("Возникла ошибка: " + err.message));
    }
  },
  mounted() {
    this.getProducts(3);
  }
};
</script>

<style scoped>
.product-cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 25px;
}

@media (max-width: 570px) {
  .product-cards {
    grid-template-columns: 1fr;
  }
}
</style>