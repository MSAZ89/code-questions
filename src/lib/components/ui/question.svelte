<script lang="ts">
	let { question = '', answers = [], correctAnswer = '', difficulty = '' } = $props();
	let answerCorrect: boolean | null = $state(null);

	function validateAnswer(selected: string) {
		if (selected === correctAnswer) {
			answerCorrect = true;
			alert('Correct!');
			console.log('Selected:', selected, 'Correct:', correctAnswer);
		} else {
			answerCorrect = false;
			alert('Incorrect. Try again.');
			console.log('Selected:', selected, 'Correct:', correctAnswer);
		}
	}
</script>

<div class="bg-gray-100 p-4">
	<p class="mb-2 text-lg font-semibold">
		{question}
		{#if difficulty}
			<span class="ml-2 rounded bg-blue-500 px-2 py-1 text-xs text-white">{difficulty}</span>
		{/if}
	</p>
	{#if answers.length > 0 && answerCorrect !== true}
		<div class="my-4 text-sm text-gray-600">
			{#if answers.length > 0}
				<div class="grid grid-cols-2 gap-2 sm:grid-cols-4">
					{#each answers as answer}
						<button
							class="rounded bg-blue-500 px-2 py-1 text-xs text-white hover:cursor-pointer hover:bg-blue-600"
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
