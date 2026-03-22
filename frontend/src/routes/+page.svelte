<script lang="ts">
	let apiStatus = $state('Checking...');

	async function checkApi() {
		try {
			const res = await fetch('/api/');
			if (res.ok) {
				apiStatus = 'Django API is reachable';
			} else {
				apiStatus = `API responded with status ${res.status}`;
			}
		} catch {
			apiStatus = 'Cannot reach Django API (is the backend running?)';
		}
	}

	$effect(() => {
		checkApi();
	});
</script>

<h1>Open LLM Eval Lab</h1>
<p>Frontend: SvelteKit | Backend: Django + DRF</p>
<p>API Status: <strong>{apiStatus}</strong></p>
<p>
	<a href="/api/docs/">API Docs (Swagger)</a> |
	<a href="/admin/">Django Admin</a>
</p>
