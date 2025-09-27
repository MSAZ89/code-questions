<script>
	import Question from '$lib/components/ui/question.svelte';

	let currentQuestion = $state(0);

	let data = [
		{
			question: 'Which value is an integer?',
			difficulty: 'easy',
			answers: ['hello', '#', 'undefined', '12'],
			correctAnswer: '12'
		},
		{
			question: 'What is the output of `typeof NaN` in JavaScript?',
			difficulty: 'medium',
			answers: ['number', 'NaN', 'undefined', 'object'],
			correctAnswer: 'number'
		},
		{
			question: 'Which method is used to add an element to the end of an array in JavaScript?',
			difficulty: 'easy',
			answers: ['push()', 'pop()', 'shift()', 'unshift()'],
			correctAnswer: 'push()'
		}
	];

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
	question={data[currentQuestion].question}
	difficulty={data[currentQuestion].difficulty}
	answers={data[currentQuestion].answers}
	correctAnswer={data[currentQuestion].correctAnswer}
/>
