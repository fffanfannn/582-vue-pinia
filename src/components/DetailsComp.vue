<template>
  <div>
    <h4>Details items</h4>
    <p>{{ detailResults }}</p>
    <p>{{ detailResults }}</p>
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
