<script lang="ts">
	var projects = [
		{
			slug: '/calculator',
			name: 'AI Powered Calculator®'
		}
	];
</script>

<div class="pl-5">
	<p>
		Here's a collection of weird and random tiny ships I've made, not significant enough to have a
		dedicated site:
	</p>
	<ul class="list-inside list-disc pl-4">
		{#each projects as project}
			<li>
				<a href={project.slug} class="text-blue-600 underline" target="_blank">{project.name}</a>
			</li>
		{/each}
	</ul>
</div>
