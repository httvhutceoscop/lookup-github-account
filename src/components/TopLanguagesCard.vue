<template>
  <h3>Top Languages Card</h3>
  <img :src="topLangsUrl" alt="" />
</template>

<script>
export default {
    props: {
        topLangsUrl: String
    }
};
</script>
