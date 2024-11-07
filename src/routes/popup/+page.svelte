<script lang="ts">
	import { onMount } from "svelte";
	let history_items: chrome.history.HistoryItem[] = [];
	onMount(() => {
		let microsecondsPerWeek = 1000 * 60 * 60 * 24 * 7;
		let oneWeekAgo = new Date().getTime() - microsecondsPerWeek;
		chrome.history.search(
			{
				text: "", // Return every history item....
				startTime: oneWeekAgo, // that was accessed less than one week ago.
			},
			function (historyItems) {
				history_items = historyItems;
			}
		);
	});
</script>

{#each history_items as { title, url }}

<p>{title} - {url}</p>
{/each}
