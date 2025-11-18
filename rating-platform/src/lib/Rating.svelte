<script lang="ts">
  import type { KeyboardEventHandler } from "svelte/elements";
  import Comment from "./Comment.svelte";

  type RatingItem = {
    id: number;
    component: typeof Comment;
    props: { text: string; isAdmin: boolean };
  };

  const {isAdmin = false} = $props(); 

  let currentId: number = 0
  let ratings: RatingItem[] = $state([])
  let inputText: string = $state("")
  let isInputLongEnough: boolean = $derived(inputText.length >= 5)

  const submit = () => {
    if (!isInputLongEnough) {
      return
    }

    let x = {
      id: currentId++,
      component: Comment,
      props: { text: inputText, isAdmin }
    }

    ratings.push(x)
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

{#each ratings.slice().reverse() as rating(rating.id)}
  <!-- <p>{rating.component}</p> -->
  <svelte:component this={rating.component} {...rating.props} />
  <!-- <Comment text={rating} isAdmin/> -->
{/each}


<style>
  .inputBox {
    margin-bottom: 10px;
  }
</style>