<script>
	import { onMount } from 'svelte';
	import Question from '$lib/components/ui/question.svelte';
	import questions from '$lib/assets/data.json';

	let data = questions;
	let isLoading = $state(true);
	let currentQuestion = $state(0);

	function getRandomQuestion() {
		return Math.floor(Math.random() * data.length);
	}

	function reloadPage() {
		location.reload();
	}

	onMount(() => {
		// Set the random question after component mounts
		currentQuestion = getRandomQuestion();
		isLoading = false;
	});
</script>

{#if isLoading}
	<div class="flex items-center justify-center p-8">
		<div class="h-8 w-8 animate-spin rounded-full border-b-2 border-green-500"></div>
		<span class="ml-3 text-gray-600">Loading question...</span>
	</div>
{:else}
	<button
		class="mb-4 rounded bg-green-500 px-4 py-2 text-white hover:cursor-pointer hover:bg-green-600"
		onclick={reloadPage}
	>
		Get Random Question
	</button>

	<Question
		question={String(data[currentQuestion].question)}
		difficulty={String(data[currentQuestion].difficulty)}
		answers={data[currentQuestion].answers.map((answer) => String(answer))}
		correctAnswer={String(data[currentQuestion].correctAnswer)}
	/>
{/if}
