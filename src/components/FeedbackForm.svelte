<script>
    export let feedbackObjList = [];

    import Button from './Button.svelte';
    import Card from './Card.svelte';
    import RatingSelect from './RatingSelect.svelte'

    import {createEventDispatcher} from 'svelte'

    let inputText = '';
    let inputRating = 10;
    let btnDisable = true;
    let message;
    const minTextLength = 10;
    
    // checking the condition for user feedback input
    const handleInput = () => {
        if (inputText.trim().length <= minTextLength) {
            message = `Text must be at least ${minTextLength} characters`;
            btnDisable = true;
        } else {
            message = null
            btnDisable = false;
        }
    }

    // get the rating value 
    // rating will be combined with text input into a obj
    // then create a custom event to return the feedback obj to App
    const extractedRating = (event) => {
        inputRating = event.detail;
    }

    const dispatchFeedbackSubmit = createEventDispatcher()

    // when invoked, activate customed event 'feedback-submitted' 
    // and return the feedback obj
    $:newFeedbackId = feedbackObjList.length + 1;
    const submitFeedback = () => {
        dispatchFeedbackSubmit(
            'feedback-submitted',
            {
                id: newFeedbackId,
                rating: inputRating,
                text: inputText,
            }
        )
    }
</script>

<Card>
    <header>
        <h2>How would you rate your service with us?</h2>
    </header>
    <form on:submit|preventDefault={submitFeedback}>
        <RatingSelect on:rating-selected={extractedRating} />
        <div class="input-group">
            <input 
                type="text" 
                on:input={handleInput} 
                bind:value={inputText} 
                placeholder="Tell us something that keeps you coming back!"
            />
            <Button 
                disable={btnDisable} 
                type="submit"
            > 
                Send 
            </Button>
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