<script>
    import Button from './Button.svelte';
    import Card from './Card.svelte';
    import RatingSelect from './RatingSelect.svelte'

    let text = '';
    let rating = 10;
    let btnDisable = true;
    let message;
    const minTextLength = 10;
    

    const handleInput = () => {
        if (text.trim().length <= minTextLength) {
            message = `Text must be at least ${minTextLength} characters`;
            btnDisable = true;
        } else {
            message = null
            btnDisable = false;
        }
    }
</script>

<Card>
    <header>
        <h2>How would you rate your service with us?</h2>
    </header>
    <form>
        <RatingSelect />
        <div class="input-group">
            <input type="text" on:input={handleInput} bind:value={text} placeholder="Tell us something that keeps you coming back!">
            <Button disable={btnDisable} type="submit"> Send </Button>
        </div>
        {#if message}
            <div class="message">
                {message}
            </div>
        {/if}
    </form>
</Card>


<style>
  header {
    max-width: 400px;
    margin: auto;
  }
  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }
  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }
  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }
  input:focus {
    outline: none;
  }
  .message{
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>