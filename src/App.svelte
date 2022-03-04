<script>
	import FeedbackList from './components/FeedbackList.svelte'
	import FeedbackStats from './components/FeedbackStats.svelte'

	let feedbackObjList = [
		{
			id: 1,
			rating: 10,
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
		},
		{
			id: 2,
			rating: 9,
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
		},
		{
			id: 3,
			rating: 8,
			text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. consequuntur vel vitae commodi alias voluptatem est voluptatum ipsa quae.',
		},
	]

	$: totalFeedbackNum = feedbackObjList.length;

	const initialValue = 0;
	$: totalRating = feedbackObjList.reduce(
		(ratingAccumulator, feedbackObj) => {
			return ratingAccumulator + feedbackObj.rating
		},
		initialValue
	) 

	$: averageRating = totalRating / totalFeedbackNum

	const handleDelete = (event) => {
		feedbackObjList = feedbackObjList.filter(
			feedbackObj => feedbackObj.id != event.detail
		)
	}
</script>

<main class="container">
	<FeedbackStats {totalFeedbackNum} {averageRating} />
	<FeedbackList {feedbackObjList} on:delete-feedback={handleDelete}/>
</main>