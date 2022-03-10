<script>
	import FeedbackForm from './components/FeedbackForm.svelte'
	import FeedbackStats from './components/FeedbackStats.svelte'
	import FeedbackList from './components/FeedbackList.svelte'

	/*
	now you have all the input: rating and text
	need to put them into an obj
	then add it the feedbackList
	*/ 
	

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

	$: averageRating = totalRating / totalFeedbackNum;

	const handleDelete = (event) => {
		feedbackObjList = feedbackObjList.filter(
			feedbackObj => feedbackObj.id != event.detail
		)
	}

	// add the new feedback obj to feedbackObjList
	const addNewFeedback = (event) => {
		const eventObj = event.detail
		console.log(eventObj);
	}
</script>

<main class="container">
	<FeedbackForm {feedbackObjList} on:feedback-submitted={addNewFeedback}/>
	<FeedbackStats {totalFeedbackNum} {averageRating} />
	<FeedbackList {feedbackObjList} on:delete-feedback={handleDelete}/>
</main>