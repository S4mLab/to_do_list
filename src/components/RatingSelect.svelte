<script>
    import {createEventDispatcher} from 'svelte'
    let selectedRating;
    const ratingList = [1,2,3,4,5,6,7,8,9,10]
    const dispatch = createEventDispatcher()
    const onChange = () => {
        dispatch('rating-selected', selectedRating)
    };

    /*
    how does select rating works?
    1. when user click a rating button, it returns a numeric value
    2. then pass this value to FeedbackForm 
    3. when FeedbackForm triggered the customed event from RatingSelect
    4. it receives the rating value and add to the text input to pass to App
    5. if user didn't choose a rating, we will set the rating as 10 as default rating
    */
</script>

<ul class="rating">
    {#each ratingList as ratingValue}
        <li>
            <input 
                type="radio" 
                name="rating" 
                id={'num'+ratingValue} 
                value={ratingValue} 
                bind:group={selectedRating} 
                on:change={onChange}
                checked
            />
            <label for={'num'+ratingValue}> {ratingValue} </label>
        </li>
    {/each}
</ul>

<style>
  .rating {
    display: flex;
    align-items: center;
    justify-content: space-around;
    margin: 30px 0;
  }
  .rating li {
    position: relative;
    background: #f4f4f4;
    width: 50px;
    height: 50px;
    padding: 10px;
    text-align: center;
    border-radius: 50%;
    font-size: 19px;
    border: 1px #eee solid;
    transition: 0.3s;
  }
  .rating li label {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 50px;
    height: 50px;
    padding: 10px;
    border-radius: 50%;
    transform: translate(-50%, -50%);
    cursor: pointer;
  }
  .rating li:hover {
    background: #ff6a95;
    color: #fff;
  }
  /* Make actual radio select invisible */
  [type='radio'] {
    opacity: 0;
  }
  /* Use the sibling select */
  [type='radio']:checked ~ label {
    background: #ff6a95;
    color: #fff;
  }
</style>

 