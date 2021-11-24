<template>
  <div class="row">
    <div class="col-12">
      <h1>{{ title }}</h1>
      <p class="lead">{{ text }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderBlock",
  props: {
    title: String,
    text: String,
  },
};
</script>