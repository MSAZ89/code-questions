<script lang="ts">
	let {
		question = '',
		answers = [],
		correctAnswer = '',
		difficulty = '',
		answerDescription = '',
		onCorrectAnswer = () => {}
	} = $props();
	let isResponseCorrect: boolean | null = $state(null);

	let wrongCount = $state(0);
	let correctCount = $state(0);

	let respondedIncorrectly = $state(false);

	function validateAnswer(selected: string) {
		if (selected === correctAnswer) {
			isResponseCorrect = true;
			if (!respondedIncorrectly) {
				correctCount += 1;
			}
			console.log('Selected:', selected, 'Correct:', correctAnswer);
		} else {
			isResponseCorrect = false;
			wrongCount += 1;
			respondedIncorrectly = true;
			console.log('Selected:', selected, 'Correct:', correctAnswer);
		}
	}

	function advanceCorrectQuestion() {
		onCorrectAnswer();
		isResponseCorrect = null; // Reset for next question
		respondedIncorrectly = false;
	}
</script>

{#if isResponseCorrect === true}
	<button
		class="rounded bg-green-500 px-2 py-1 text-white hover:cursor-pointer hover:bg-green-600"
		onclick={advanceCorrectQuestion}
	>
		Next Question
	</button>
{/if}

<div class="mt-2 bg-gray-100 p-4">
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
		</div>
	</div>
	{#if answers.length > 0}
		<div class="my-4 text-sm text-gray-600">
			{#if answers.length > 0}
				<div class="grid grid-cols-2 gap-2 sm:grid-cols-2">
					{#each answers as answer}
						<button
							disabled={isResponseCorrect === true}
							class="rounded px-2 py-4 text-white hover:cursor-pointer sm:text-xl
		{isResponseCorrect !== null
								? answer === correctAnswer
									? 'bg-green-500 shadow-lg shadow-green-200 disabled:cursor-not-allowed disabled:bg-green-500 disabled:text-white'
									: 'bg-gray-300 text-gray-500 disabled:cursor-not-allowed disabled:bg-gray-300 disabled:text-gray-500'
								: 'bg-blue-500 hover:bg-blue-600'}"
							onclick={() => validateAnswer(answer)}>{answer}</button
						>
					{/each}
				</div>
			{:else}
				No answers provided.
			{/if}
		</div>
	{/if}
	{#if isResponseCorrect === true}
		<p class="mt-2 text-center text-xl font-bold text-green-600">Correct!</p>
		<p class="mt-2 text-center text-gray-700">{answerDescription}</p>
	{:else if isResponseCorrect === false}
		<p class="mt-2 text-center text-xl font-bold text-red-600">Incorrect. Try again.</p>
	{/if}
</div>

<div class="flex flex-wrap gap-4 p-2">
	<p class="mb-2 text-sm text-green-600">
		Correct: {correctCount}
	</p>
	<p class="mb-2 text-sm text-red-600">
		Wrong: {wrongCount}
	</p>
	<p class="mb-2 text-sm text-yellow-600">
		Total Attempts: {correctCount + wrongCount}
	</p>
</div>
