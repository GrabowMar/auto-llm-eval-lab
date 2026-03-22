<script lang="ts">
	import { Button } from '$lib/components/ui/button';
	import * as Card from '$lib/components/ui/card';

	let apiStatus = $state('Checking...');
	let apiOk = $state(false);

	async function checkApi() {
		try {
			const res = await fetch('/api/');
			if (res.ok) {
				apiStatus = 'Django API is reachable';
				apiOk = true;
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

<div class="flex min-h-screen items-center justify-center p-4">
	<Card.Card class="w-full max-w-md">
		<Card.CardHeader>
			<Card.CardTitle>Open LLM Eval Lab</Card.CardTitle>
			<Card.CardDescription>Frontend: SvelteKit | Backend: Django + DRF</Card.CardDescription>
		</Card.CardHeader>
		<Card.CardContent>
			<p class="text-sm">
				API Status:
				<span class={apiOk ? 'font-medium text-green-600 dark:text-green-400' : 'font-medium text-muted-foreground'}>
					{apiStatus}
				</span>
			</p>
		</Card.CardContent>
		<Card.CardFooter class="gap-2">
			<Button variant="outline" onclick={() => window.open('/api/docs/', '_blank')}>
				API Docs
			</Button>
			<Button variant="outline" onclick={() => window.open('/admin/', '_blank')}>
				Django Admin
			</Button>
		</Card.CardFooter>
	</Card.Card>
</div>
