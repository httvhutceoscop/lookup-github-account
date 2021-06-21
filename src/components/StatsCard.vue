<template>
  <h3>GitHub Stats Card</h3>
  <p>
    <em
      >Note: Available ranks are S+ (top 1%), S (top 25%), A++ (top 45%), A+
      (top 60%), and B+ (everyone). The values are calculated by using the
      <a
        target="_blank"
        href="https://en.wikipedia.org/wiki/Cumulative_distribution_function"
      >
        cumulative distribution function</a
      >
      using commits, contributions, issues, stars, pull requests, followers, and
      owned repositories.
    </em>
  </p>
  <img :src="statsUrl" alt="" />
</template>

<script>
export default {
    props: {
        statsUrl: String
    }
};
</script>
