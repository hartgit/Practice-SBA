<script>
  import { onMount } from "svelte";

  let countries = [];

  function dataFetch() {
    fetch(
      `https://gist.githubusercontent.com/dfenders/8ceec1cc3ec2d05c9ac7ebbe58e03774/raw/fea0abe2f813a4790d5626eeb87c99a0775a3620/olympics.json`
    )
      .then((res) => res.json())
      .then((data) => {
        console.log(data);

        countries = data.sort((a, b) =>
          (a.gold + a.silver + a.bronze < b.gold + b.silver + b.bronze ? 1 : -1)).splice(0, 10);
      });
  }

  onMount(async () => {
    dataFetch();
  });
</script>

<div class="container">
  {#each countries as country}
    <h1>{country.country}</h1>

    <section class="medals">
      {#each { length: country.gold } as _, i}
        <div class="goldMedal" />
      {/each}
      {#each { length: country.silver } as _, i}
        <div class="silverMedal" />
      {/each}
      {#each { length: country.bronze } as _, i}
        <div class="bronzeMedal" />
      {/each}
    </section>
  {/each}
</div>

<style>
  .medals {
    display: flex;
    flex-wrap: wrap;
  }
  .goldMedal {
    width: 20px;
    height: 20px;
    background: gold;
    border-radius: 100%;
  }

  .silverMedal {
    width: 20px;
    height: 20px;
    background: silver;
    border-radius: 100%;
  }

  .bronzeMedal {
    width: 20px;
    height: 20px;
    background: tan;
    border-radius: 100%;
  }
</style>
