<script lang="ts">
	let {
		question = '',
		answers = [],
		correctAnswer = '',
		difficulty = '',
		onCorrectAnswer = () => {}
	} = $props();
	let answerCorrect: boolean | null = $state(null);

	let wrongCount = $state(0);
	let correctCount = $state(0);

	function validateAnswer(selected: string) {
		if (selected === correctAnswer) {
			answerCorrect = true;
			correctCount += 1;
			console.log('Selected:', selected, 'Correct:', correctAnswer);
		} else {
			answerCorrect = false;
			wrongCount += 1;
			console.log('Selected:', selected, 'Correct:', correctAnswer);
		}
	}

	function advanceCorrectQuestion() {
		onCorrectAnswer();
		answerCorrect = null; // Reset for next question
	}
</script>

<div>
	{#if answerCorrect === true}
		<button
			class="mb-4 rounded bg-green-500 px-2 py-1 text-white hover:cursor-pointer hover:bg-green-600"
			onclick={advanceCorrectQuestion}
		>
			Next Question
		</button>
	{/if}
</div>

<div class="bg-gray-100 p-4">
	<div class="mb-2 flex items-center text-lg font-semibold">
		<div>
			<h2 class="mb-2 text-2xl font-bold">
				{question}
				{#if difficulty}
					<span
						class="w-[fit-content] rounded bg-gray-900 px-2 py-0 pb-1 text-sm font-light text-white"
					>
						{difficulty}
					</span>
				{/if}
			</h2>
			{#if answerCorrect === true}
				<div>
					<code class="bg-black px-2 text-white">Answer: {correctAnswer}</code>
				</div>
			{/if}
		</div>
	</div>
	{#if answers.length > 0 && answerCorrect !== true}
		<div class="my-4 text-sm text-gray-600">
			{#if answers.length > 0}
				<div class="grid grid-cols-2 gap-2 sm:grid-cols-2">
					{#each answers as answer}
						<button
							class="rounded bg-blue-500 px-2 py-4 text-white hover:cursor-pointer hover:bg-blue-600 sm:text-xl"
							onclick={() => validateAnswer(answer)}>{answer}</button
						>
					{/each}
				</div>
			{:else}
				No answers provided.
			{/if}
		</div>
	{/if}
	{#if answerCorrect === true}
		<p class="mt-2 text-green-600">Correct!</p>
	{:else if answerCorrect === false}
		<p class="mt-2 text-center text-red-600">Incorrect. Try again.</p>
	{/if}
</div>

<div class="flex flex-wrap gap-4 p-2">
	<p class="mb-2 text-sm text-green-600">
		Correct: {correctCount}
	</p>
	<p class="mb-2 text-sm text-red-600">
		Wrong: {wrongCount}
	</p>
</div>
