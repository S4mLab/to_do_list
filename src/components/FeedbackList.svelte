<script>
    import FeedbackItem from './FeedbackItem.svelte'
    export let feedbackObjList = [];

    // send feedback items isn't imbeded in FeedbackList 
    // we can call the event 'delete-feedback' from FeedbackItem
    // in order to delete an feedback card, the App need to know the id of the feedback obj that it need to remove from the list
    // when the app got the id, it then remove that specific feedback from the list
    // update the list then pass it to FeedbackList

</script>

{#each feedbackObjList as feedbackObj (feedbackObj.id)}
    <FeedbackItem {feedbackObj} on:delete-feedback/>
{/each}

