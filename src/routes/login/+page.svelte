<script lang="ts">
	import { goto } from "$app/navigation";
	import Button from "$lib/components/Button.svelte";
	import { updateMySecretKey } from "$lib/ws.svelte";
	import * as bip39 from "@scure/bip39";
	import { wordlist } from "@scure/bip39/wordlists/english";

	let secretKey = $state("");
	const isValid = $derived(bip39.validateMnemonic(secretKey, wordlist));
</script>

<div class="flex min-h-screen max-w-screen flex-col items-center justify-center gap-2">
	<img src="/pexe-concord.png" alt="" class="hidden xl:block xl:mb-10">
	<div class="bg-[#393A41] w-full h-screen overflow-y-auto pt-4 md:text-2xl xl:max-w-[800px] xl:max-h-[370px] xl:rounded-lg">
		<img src="/pexe-concord.png" alt="" class="block max-w-[300px] mx-auto md:max-w-[500px] xl:hidden">
		<div class="flex flex-col items-center mt-4 gap-3">
			<span class="font-bold text-xl md:text-4xl lg:text-4xl">Welcome back freedom enjoyer!</span>
			<p class="text-[#dcdcdf] text-md">proceed with the login below.</p>
		</div>

		<div class="flex flex-col gap-4 mt-10">
			<label class="flex flex-col items-center">
				<input 
					placeholder="Insert your 12 words secret key here!" 
					class="gray-500 border border-gray-500 min-w-[300px] md:min-w-[450px]" 
					type="text" 
					bind:value={secretKey}
				/>
			</label>
			<div class="login-btn-width flex flex-col items-center">
				<Button
					disabled={!isValid}
					onclick={() => {
						updateMySecretKey(secretKey);

						goto("/")
					}}>Log In</Button>
			</div>
		</div>
		<div class="flex flex-col items-center mt-4">
			<p class="text-[#ABACB2]">New to concord? <a href="/register" class="text-blue-400 underline hover:no-underline">Register instead</a></p>
		</div>
	</div>
</div>
