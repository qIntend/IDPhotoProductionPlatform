<template>
  <div>
    <hero></hero>
    <TabsSection></TabsSection>
  </div>
</template>P
<script>
import Hero from "./components/Hero";
import TabsSection from "./components/JavascriptComponents/TabsSection";

export default {
  name: "components",
  components: {
    Hero,
    TabsSection
  }
};
</script>
