<script lang="ts">
    const {text = "", rating = 5, isAdmin = false} = $props(); 
    let likes = $state(0)
</script>

<div class="commentField">
    <p>{text}</p>
    
    <div class="contol">
        <p>{rating}</p>
        <p class:positive={likes>0} class:negative={likes<0}>{likes}</p>
        {#if isAdmin}
        <div class="buttons">
            <button>🟥</button>
            <button onclick={() => {likes++}}>👍</button>
            <button onclick={() => {likes--}}>👎</button>            
        </div>
        {/if}
    </div>
</div>

<style>
    .commentField {
        background-color: rgb(113, 113, 113);
        display: flex;
        gap: 50px;
        padding: 10px;
    }

    .contol{
        display: flex;
        gap: 20px;
        margin-left: auto;
        margin-right: 10px;
    }

    .buttons{
        display: flex;
        gap: 1px;
        margin-left: auto;
    }

    .positive {
        color: mediumaquamarine;
    }

    .negative {
        color: tomato;
    }
</style>