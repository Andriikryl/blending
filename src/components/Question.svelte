<script>
  import Accordion from "./Accordion.svelte";
  import AccordionItem from "./AccordionItem.svelte";

  const items = [
    {
      title: "How to normalised values between 0 and 1?",
      content: `Exemple: background-color: rgb(244,63,94); --->Divide by 255 each number: 244 / 255 = 0.96; 63/255 = 0.25; 94/255 = 0.37;
      Output: (0.96, 0.25, 0.37)
      `,
    },
    {
      title: "How to invert the value?",
      content: `
          Exemple: (0.96, 0.25, 0.37); ---> Subtract 1 from each number: 1 - 0.96 = 0.04, 1 - 0.25 = 0.75, 1 - 0.37 = 0.63;
          Output: (0.04, 0.75, 0.63)
        `,
    },
    {
      title: "How to clamp value between 0 and 1?",
      content: `
        function clamp(value: number, min = 0, max = 1) {
    return Math.min(Math.max(value, min), max);
  }
        `,
    },
    {
      title: "How to return only positive numbers?",
      content: `
      You can use: Math.abs() - static method returns the absolute value of a number.
        `,
    },
  ];
</script>

<section class="questions">
  <div class="container">
    <div class="content__box">
      <Accordion collapse --accordion-width="100ch">
        {#each items as item, i}
          <AccordionItem open={i === 0}>
            <svelte:fragment slot="title">{item.title}</svelte:fragment>
            <svelte:fragment slot="content">{item.content}</svelte:fragment>
          </AccordionItem>
        {/each}
      </Accordion>
    </div>
  </div>
</section>

<style>
  .questions {
    margin-block-end: 30px;
  }
  .content__box {
    margin-block: 50px;
    max-width: 800px;
    display: flex;
    justify-content: center;
    margin-inline: auto;
  }
</style>
