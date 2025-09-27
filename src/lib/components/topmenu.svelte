<script lang="ts">
	import { page } from '$app/stores';

	// Function to check if current route matches href
	function isActive(href: string): boolean {
		if (href === '/') {
			return $page.url.pathname === '/';
		}
		return $page.url.pathname.startsWith(href);
	}
</script>

<div
	class="mx-auto mb-4 flex flex-wrap items-center justify-center space-x-4 text-sm text-white underline underline-offset-2"
>
	<a
		href="/javascript"
		class:text-yellow-400={isActive('/javascript')}
		class:font-bold={isActive('/javascript')}
	>
		JavaScript
	</a>
	<a
		href="/csharp"
		class:text-yellow-400={isActive('/csharp')}
		class:font-bold={isActive('/csharp')}
	>
		C#
	</a>
	<a href="/" class:text-yellow-400={isActive('/')} class:font-bold={isActive('/')}> Home </a>
</div>
