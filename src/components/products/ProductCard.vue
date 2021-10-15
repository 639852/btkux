<template>
  <div class="product-cards__item product">
    <img :src="product.image.file.url" class="product__img" alt="Название" />
    <div class="product__content">
      <h5 class="product__name">{{ product.title }}</h5>
      <h6 class="product__price">
        {{
          product.price
            .toString()
            .replace(/(\d{1,3}(?=(?:\d\d\d)+(?!\d)))/g, "$1" + " ") + " ₽"
        }}
      </h6>
      <a
        href="#"
        class="product__link"
        v-for="(color, index) of product.colors"
        :key="index"
        :style="{ color: color.code }"
        >{{ color.title }}</a
      >
    </div>
  </div>
</template>

<script>
export default {
  props: ["product"]
};
</script>

<style scoped>
.product {
  display: flex;
  flex-direction: column;
  padding: 20px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  border-radius: 5px;
}

.product__content {
  margin-top: 15px;
}

.product__img {
  display: block;
  max-width: 100%;
  max-height: 450px;
  margin: auto;
}

.product__price {
  color: #6c757d;
}

.product__link {
  transition: 0.2s;
}

.product__link:not(:last-child) {
  margin-right: 20px;
}

.product__link:hover {
  text-decoration: none;
  opacity: 0.7;
}
</style>