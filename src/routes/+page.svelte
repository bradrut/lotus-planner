<script>
  /**
   * The Y translation values for each category in the categories array, meant to give a parabolic effect to the category
   * buttons below the lotus image.
   */
  $: categoryTranslationValues = {
    0: 0,
    1: 50,
    2: 100,
    3: 50,
    4: 0,
  };

  // TODO: Decouple the translation values from the specific categories themselves
  $: categories = [
    { category: "Intellectual", translationValue: categoryTranslationValues[0], shadowColor: "" },
    { category: "Social", translationValue: categoryTranslationValues[1], shadowColor: "" },
    { category: "Spiritual", translationValue: categoryTranslationValues[2], shadowColor: "" },
    { category: "Physical", translationValue: categoryTranslationValues[3], shadowColor: "#06b6d4" },
    { category: "Hobbies", translationValue: categoryTranslationValues[4], shadowColor: "" },
  ];
</script>

<!-- TODO: Finish making fully reponsive -->
<div class="grid h-full grid-cols-3 content-center">
  <div class="col-span-3">
    <h1 class="text-4xl text-center font-extralight -translate-y-24">Cultivate your garden.</h1>
    <img src="/lotus.png" alt="Lotus flower" class="box-content lotus-img" />
    <div class="grid grid-cols-5 gap-24">
      {#each categories as category}
        <button
          class="bg-transparent text-white py-8 px-4 rounded-full font-extralight text-xl"
          style="transform: translateY({category.translationValue}px)">
          {category.category}
        </button>
      {/each}
    </div>
  </div>
</div>

<style lang="postcss">
  .lotus-img {
    max-height: 240px;
    width: auto;
    height: auto;
    margin-left: auto;
    margin-right: auto;
  }

  .category:hover {
    -webkit-transform: scale(1.05);
  }
</style>
