<script lang="ts">
  import type { KeyboardEventHandler } from "svelte/elements";
  import Comment from "./Comment.svelte";

  const {isAdmin = false} = $props(); 

  let ratings: string[] = $state([])
  let inputText: string = $state("")
  let isInputLongEnough: boolean = $derived(inputText.length >= 5)

  const submit = () => {
    if (!isInputLongEnough) {
      return
    }

    let x = Comment

    ratings.push(inputText)
    inputText = ""
  }

  function handleInputKey(k: KeyboardEvent){
    if (k.key === "Enter"){
          submit()
    } 
  }
</script>


<h1>Please rate Svelte</h1>

<input class="inputBox" placeholder="Type some comment" bind:value={inputText} maxlength="100" onkeydown={handleInputKey}>

<button disabled={!isInputLongEnough} onclick={submit}>
  Submit
</button>

{#each ratings.slice().reverse() as rating}
  <!-- <p>{rating}</p> -->
  <Comment text={rating} isAdmin/>
{/each}


<style>
  .inputBox {
    margin-bottom: 10px;
  }
</style>