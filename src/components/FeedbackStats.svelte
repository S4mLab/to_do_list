<script>
    export let totalFeedbackNum;
    export let averageRating;
</script>

<div class="feedback-stats">
    <h4>{totalFeedbackNum} Reviews</h4>
    <h4> Average Rating: {averageRating}</h4>
</div>

<style>
    .feedback-stats {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
</style>

