<script>
    import FeedbackItem from './FeedbackItem.svelte'
    export let feedbackObjList = [];
</script>

{#each feedbackObjList as feedbackObj (feedbackObj.id)}
    <FeedbackItem {feedbackObj}/>
{/each}