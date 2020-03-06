<template>
  <div class="home">
    <Checklist />
  </div>
</template>

<script>
// @ is an alias to /src
import Checklist from "@/components/Checklist.vue";

export default {
  name: "Home",
  components: {
    Checklist
  }
};
</script>
