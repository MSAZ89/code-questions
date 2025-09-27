<script>
	import Question from '$lib/components/ui/question.svelte';
	import questions from '$lib/assets/data.json';

	let currentQuestion = $state(0);

	let data = questions;

	function getRandomQuestion() {
		currentQuestion = Math.floor(Math.random() * data.length);
		console.log('Current Question Index:', currentQuestion);
	}
</script>

<button
	class="mb-4 rounded bg-green-500 px-4 py-2 text-white hover:cursor-pointer hover:bg-green-600"
	onclick={getRandomQuestion}
>
	Get Random Question
</button>

<Question
	question={String(data[currentQuestion].question)}
	difficulty={String(data[currentQuestion].difficulty)}
	answers={data[currentQuestion].answers.map((answer) => String(answer))}
	correctAnswer={String(data[currentQuestion].correctAnswer)}
/>
