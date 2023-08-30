<template>
  <div>
    <h4>Details items</h4>
    <p>{{ detailResults.name }}</p>
    <p>{{ detailResults.age }}</p>
  </div>
</template>

<script>
export default {
  name: "DetailsComp",
  props: {
    detailResults: Object,
  },
};
</script>
