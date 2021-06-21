<template>
  <h3>Wakatime Week Stats</h3>
  <img :src="wakatimeUrl" alt="" />
</template>

<script>
export default {
    props: {
        wakatimeUrl: String
    }
};
</script>
