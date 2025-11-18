<script lang="ts">
    const {text = "", isAdmin = false} = $props(); 
    let likes = $state(0)
</script>

<div class="commentField">
    <p>{text}</p>

    <p class:positive={likes>0} class:negative={likes<0}>{likes}</p>

    {#if isAdmin}
        <div class="buttons">
            <button>🟥</button>
            <button onclick={() => {likes++}}>👍</button>
            <button onclick={() => {likes--}}>👎</button>            
        </div>
    {/if}
</div>

<style>
    .commentField {
        background-color: rgb(113, 113, 113);
        display: flex;
        gap: 50px;
        padding: 10px;
    }

    .buttons{
        display: flex;
        gap: 1px;
    }

    .positive {
        color: mediumaquamarine;
    }

    .negative {
        color: tomato;
    }
</style>