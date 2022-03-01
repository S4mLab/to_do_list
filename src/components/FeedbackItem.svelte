<script>
    import Card from "./Card.svelte";
    import {createEventDispatcher} from 'svelte'
    export let feedbackObj = {};
    
    const dispatcher = createEventDispatcher()

    const handleDelete = (feedbackId) => {
        dispatcher('delete-feedback', feedbackId)
    }

    // so in order to delete a feedback, 
    // we need to transfer the state back to App.svelte
    // we need somehow send the state up
    // so how we do it is we dispatch a custom event
    
</script>

<Card>
    <div class="num-display">
        {feedbackObj.rating}
    </div>
    <button class="close" on:click={handleDelete(feedbackObj.id)}>
        X
    </button>
    <p class="text-display">
        {feedbackObj.text}
    </p>
</Card>

<style>
  .num-display {
    position: absolute;
    top: -10px;
    left: -10px;
    width: 50px;
    height: 50px;
    background: #ff6a95;
    color: #fff;
    border: 1px #eee solid;
    border-radius: 50%;
    padding: 10px;
    text-align: center;
    font-size: 19px;
  }
  .close {
    position: absolute;
    top: 10px;
    right: 20px;
    cursor: pointer;
    background: none;
    border: none;
  }
</style>
