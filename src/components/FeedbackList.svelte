<script>
    import FeedbackItem from './FeedbackItem.svelte'
    export let feedbackObjList = [];

    // send feedback items isn't imbeded in FeedbackList 
    // we can call the event 'delete-feedback' from FeedbackItem

</script>

{#each feedbackObjList as feedbackObj (feedbackObj.id)}
    <FeedbackItem {feedbackObj} on:delete-feedback/>
{/each}

