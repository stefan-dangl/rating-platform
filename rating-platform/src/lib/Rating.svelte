<script lang="ts">
  import Comment from "./Comment.svelte";

  type RatingItem = {
    id: number;
    props: { text: string; rating: number; isAdmin: boolean };
  };

  const {isAdmin = false} = $props(); 

  let currentId: number = 0
  let ratings: RatingItem[] = $state([])
  let inputText: string = $state("")
  let radioValue: string = $state("5")
  let isInputLongEnough: boolean = $derived(inputText.length >= 5)

  const submit = () => {
    if (!isInputLongEnough) {
      return
    }

    ratings.push({
      id: currentId++,
      props: { text: inputText, rating: Number(radioValue), isAdmin }
    })

    inputText = ""
  }

  function handleInputKey(k: KeyboardEvent){
    if (k.key === "Enter"){
          submit()
    } 
  }
</script>


<h1 style="color: orangered">Rate Svelte</h1>

<label>
  <input type="radio" name="rating" value="1" bind:group={radioValue} />
  1
</label>
<label>
  <input type="radio" name="rating" value="2" bind:group={radioValue} />
  2
</label>
<label>
  <input type="radio" name="rating" value="3" bind:group={radioValue} />
  3
</label>
<label>
  <input type="radio" name="rating" value="4" bind:group={radioValue} />
  4
</label>
<label>
  <input type="radio" name="rating" value="5" bind:group={radioValue} />
  5
</label>

<br>
<input class="inputBox" placeholder="Type some comment" bind:value={inputText} maxlength="100" onkeydown={handleInputKey}>

<button disabled={!isInputLongEnough} onclick={submit}>
  Submit
</button>

{#each ratings.slice().reverse() as rating(rating.id)}
  <Comment {...rating.props} />
{/each}


<style>
  .inputBox {
    margin-bottom: 10px;
  }
</style>