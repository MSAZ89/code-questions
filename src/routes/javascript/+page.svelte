<script lang="ts">
	import { onMount } from 'svelte';
	import Question from '$lib/components/ui/question.svelte';
	import questions from '$lib/assets/jsdata.json';

	let data = questions;
	let isLoading = $state(true);
	let currentQuestion = $state(0);
	let usedQuestions = $state<number[]>([]);
	let allQuestionsCompleted = $state(false);

	function getRandomQuestion() {
		// Get available questions (not used yet)
		const availableIndices = data
			.map((_, index) => index)
			.filter((index) => !usedQuestions.includes(index));

		// If no available questions, mark as completed
		if (availableIndices.length === 0) {
			allQuestionsCompleted = true;
			return null;
		}

		// Pick random from available
		const randomIndex = Math.floor(Math.random() * availableIndices.length);
		return availableIndices[randomIndex];
	}

	function getNextQuestion() {
		const newQuestion = getRandomQuestion();
		if (newQuestion !== null) {
			usedQuestions = [...usedQuestions, newQuestion];
			currentQuestion = newQuestion;
		}
	}

	onMount(() => {
		// Set the random question after component mounts
		const initialQuestion = getRandomQuestion();
		if (initialQuestion !== null) {
			usedQuestions = [initialQuestion];
			currentQuestion = initialQuestion;
		}
		isLoading = false;
	});
</script>

{#if isLoading}
	<div class="flex items-center justify-center p-8">
		<div class="h-8 w-8 animate-spin rounded-full border-b-2 border-green-500"></div>
		<span class="ml-3 text-gray-600">Loading question...</span>
	</div>
{:else if allQuestionsCompleted}
	<div class="p-8 text-center">
		<h2 class="mb-4 text-2xl font-bold text-green-600">🎉 Congratulations!</h2>
		<p class="mb-4 text-lg text-gray-700">You've completed all {data.length} questions!</p>
		<button
			class="rounded bg-blue-500 px-6 py-3 text-white hover:cursor-pointer hover:bg-blue-600"
			onclick={() => location.reload()}
		>
			Start Over
		</button>
	</div>
{:else}
	<span class="mb-4 text-xl text-gray-300">
		Progress: {usedQuestions.length} / {data.length}
	</span>

	<Question
		question={String(data[currentQuestion].question)}
		difficulty={String(data[currentQuestion].difficulty)}
		answers={data[currentQuestion].answers.map((answer) => String(answer))}
		correctAnswer={String(data[currentQuestion].correctAnswer)}
		onCorrectAnswer={getNextQuestion}
	/>
{/if}
