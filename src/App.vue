<template>
  <main>
    <Form />

    <Products />
  </main>
</template>

<script>
import "bootstrap/dist/css/bootstrap.min.css";
import Form from "./components/form/Form.vue";
import Products from "./components/products/Products.vue";

export default {
  name: "App",
  components: { Form, Products }
};
</script>
