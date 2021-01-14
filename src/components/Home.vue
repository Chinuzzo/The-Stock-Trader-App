<template>
  <div>
    <h1>Trade or View your Portfolio</h1>
    <h6>You may <strong>Save & Load</strong> your data</h6>
    <h6>Click on <strong>End Day</strong> to begin a new day!</h6>
    <hr />
    <p>Your Funds: {{ funds | currency }}</p>
  </div>
</template>

<script>
export default {
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
  },
};
</script>
