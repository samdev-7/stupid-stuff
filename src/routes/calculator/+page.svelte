<script lang="ts">
	let a = 0;
	let b = 0;
	let result = 'Ask something to get a result!';
	let isLoading = false;

	function ask() {
		isLoading = true;
		let prompt = `What is ${a} + ${b} equal to? Provide the result and explain how you got to the result. The result needs to be in plain text, no html or markdown.`;
		let body = {
			messages: [{ role: 'user', content: prompt }]
		};
		fetch('https://ai.hackclub.com/chat/completions', {
			method: 'POST',
			body: JSON.stringify(body),
			headers: {
				'Content-Type': 'application/json'
			}
		}).then((res) => {
			res.json().then((data) => {
				console.log(data);
				isLoading = false;
				result = data.choices[0].message.content;
			});
		});
	}
</script>

<div class="flex min-h-screen items-center justify-center bg-gray-100">
	<div class="w-xl space-y-5 border border-gray-200 bg-white p-8 shadow-sm">
		<div>
			<h1 class="text-2xl font-medium">
				<span class="bg-gradient-to-br from-blue-500 to-purple-500 bg-clip-text text-transparent"
					>AI</span
				> Powered Calculator®
			</h1>
			<p>Addition mode</p>
		</div>
		<div class="space-y-3">
			<div class="flex space-x-6">
				<input
					type="number"
					name="a"
					id="a"
					class="w-20 grow rounded-sm border border-gray-400 px-2 py-0.5"
					bind:value={a}
				/>
				<p>+</p>
				<input
					type="number"
					name="b"
					id="b"
					class="w-20 grow rounded-sm border border-gray-400 px-2 py-0.5"
					bind:value={b}
				/>
			</div>
			<button
				class="w-full rounded-sm border border-gray-300 px-2 py-0.5 shadow"
				on:click={ask}
				disabled={isLoading}
			>
				{isLoading ? 'Loading...' : 'Ask ChatGPT'}
			</button>
		</div>
		<div>
			<p class="font-medium">Result:</p>
			<div class="rounded-md bg-gray-100 p-1">
				<code>{isLoading ? 'Loading...' : result}</code>
			</div>
		</div>
	</div>
</div>
