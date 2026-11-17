<script lang="ts">
	import { enhance } from '$app/forms';
	import { projects, profile } from '$lib/data';
	import ProjectRow from '$lib/components/ProjectRow.svelte';

	type Theme = 'light' | 'dark';
	type Status = 'idle' | 'loading' | 'success' | 'error';

	let theme: Theme = $state('light');
	let status: Status = $state('idle');
	let menuOpen = $state(false);

	function toggleTheme() {
		theme = theme === 'light' ? 'dark' : 'light';
	}
</script>

<svelte:head>
	<title>Portfolio | Olivia Oktarina</title>
	<meta
		name="description"
		content="Portfolio pribadi siswa SMK jurusan PPLG."
	/>
</svelte:head>

<div
	class:dark={theme === 'dark'}
	class="min-h-dvh overflow-hidden bg-[#faf9f6] text-[#242424] transition-colors duration-300 dark:bg-[#151515] dark:text-white"
>
	<!-- NAVBAR -->
	<header
		class="sticky top-0 z-50 border-b border-black/5 bg-[#faf9f6]/90 backdrop-blur-xl transition-colors duration-300 dark:border-white/10 dark:bg-[#151515]/90"
	>
		<div
			class="mx-auto flex h-[76px] max-w-[1400px] items-center justify-between px-6 lg:px-16"
		>
			<a href="#home" class="flex items-center gap-3">
				<div
					class="flex h-10 w-10 items-center justify-center rounded-xl bg-[#ff7043] text-lg font-black text-white"
				>
					N.
				</div>

				<div>
					<p class="text-sm font-bold tracking-tight">Olivia Oktarina</p>
					<p class="text-[10px] tracking-[2px] text-gray-400">MY PORTFOLIO</p>
				</div>
			</a>

			<nav class="hidden items-center gap-9 md:flex">
				<a href="#home" class="text-sm text-gray-500 transition hover:text-[#ff7043] dark:text-gray-300">Home</a>
				<a href="#proyek" class="text-sm text-gray-500 transition hover:text-[#ff7043] dark:text-gray-300">Proyek</a>
				<a href="#tentang" class="text-sm text-gray-500 transition hover:text-[#ff7043] dark:text-gray-300">Tentang</a>
				<a href="#kontak" class="text-sm text-gray-500 transition hover:text-[#ff7043] dark:text-gray-300">Kontak</a>
			</nav>

			<div class="flex items-center gap-3">
				<!-- THEME BUTTON -->
				<button
					type="button"
					aria-label="Ganti tema"
					onclick={toggleTheme}
					class="flex h-10 w-10 items-center justify-center rounded-full border border-black/10 transition hover:bg-black/5 dark:border-white/15 dark:hover:bg-white/10"
				>
					{#if theme === 'light'}
						<!-- MOON ICON -->
						<svg
							width="19"
							height="19"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="1.7"
						>
							<path d="M21 12.8A9 9 0 1 1 11.2 3a7 7 0 0 0 9.8 9.8Z" />
						</svg>
					{:else}
						<!-- SUN ICON -->
						<svg
							width="19"
							height="19"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="1.7"
						>
							<circle cx="12" cy="12" r="4" />
							<path
								d="M12 2v2m0 16v2M4.93 4.93l1.42 1.42m11.3 11.3 1.42 1.42M2 12h2m16 0h2M4.93 19.07l1.42-1.42m11.3-11.3 1.42-1.42"
							/>
						</svg>
					{/if}
				</button>

				<!-- MOBILE MENU BUTTON -->
				<button
					type="button"
					aria-label="Buka menu"
					onclick={() => (menuOpen = !menuOpen)}
					class="flex h-10 w-10 items-center justify-center rounded-full border border-black/10 transition hover:bg-black/5 dark:border-white/15 dark:hover:bg-white/10 md:hidden"
				>
					<svg
						width="20"
						height="20"
						viewBox="0 0 24 24"
						fill="none"
						stroke="currentColor"
						stroke-width="1.7"
					>
						{#if menuOpen}
							<path d="m6 6 12 12M18 6 6 18" />
						{:else}
							<path d="M4 7h16M4 12h16M4 17h16" />
						{/if}
					</svg>
				</button>
			</div>
		</div>

		<!-- MOBILE NAVIGATION -->
		{#if menuOpen}
			<nav
				class="flex flex-col gap-5 border-t border-black/5 bg-[#faf9f6] px-7 py-6 text-sm transition-colors duration-300 dark:border-white/10 dark:bg-[#151515] md:hidden"
			>
				<a onclick={() => (menuOpen = false)} href="#home">Home</a>
				<a onclick={() => (menuOpen = false)} href="#proyek">Proyek</a>
				<a onclick={() => (menuOpen = false)} href="#tentang">Tentang</a>
				<a onclick={() => (menuOpen = false)} href="#kontak">Kontak</a>
			</nav>
		{/if}
	</header>

	<!-- HERO -->
	<section
		id="home"
		class="relative mx-auto max-w-[1400px] px-6 pb-24 pt-20 transition-colors duration-300 lg:px-16 lg:pb-32 lg:pt-32"
	>
		<div
			class="pointer-events-none absolute right-[8%] top-20 -z-0 h-64 w-64 rounded-full bg-[#ff7043]/10 blur-[100px]"
		></div>

		<div class="relative z-10">
			<div
				class="mb-8 inline-flex items-center gap-3 rounded-full border border-[#ff7043]/20 bg-[#ff7043]/5 px-4 py-2"
			>
				<span class="h-2 w-2 animate-pulse rounded-full bg-green-500"></span>
				<span class="text-xs font-medium tracking-wide text-[#ff7043]">
					HELLO! WELCOME TO MY PORTFOLIO
				</span>
			</div>

			<h1
				class="max-w-[1100px] text-[70px] font-black leading-[0.95] tracking-[-3px] sm:text-7xl lg:text-[125px] lg:tracking-[-7px]"
			>
				Olivia
				<br />
				<span class="text-[#ff7043]">Oktarina</span>
			</h1>

			<div class="mt-12 flex flex-col justify-between gap-10 lg:flex-row lg:items-end">
				<div class="max-w-[520px]">
					<p class="text-lg leading-relaxed text-gray-500 dark:text-gray-400 lg:text-xl">
						Halo! Saya seorang siswa SMK jurusan PPLG yang tertarik dengan dunia teknologi,
						pengembangan aplikasi, dan desain antarmuka digital.
					</p>

					<div class="mt-8 flex flex-wrap gap-4">
						<a
							href="#proyek"
							class="group flex h-14 items-center gap-3 rounded-xl bg-[#ff7043] px-7 text-sm font-semibold text-white shadow-lg shadow-[#ff7043]/20 transition hover:-translate-y-1 hover:bg-[#ed5e32]"
						>
							Lihat Proyek Saya
							<svg
								class="transition group-hover:translate-x-1"
								width="18"
								height="18"
								viewBox="0 0 24 24"
								fill="none"
								stroke="currentColor"
								stroke-width="2"
							>
								<path d="M5 12h14m-7-7 7 7-7 7" />
							</svg>
						</a>

						<a
							href="#kontak"
							class="flex h-14 items-center rounded-xl border border-black/10 px-7 text-sm font-semibold transition hover:bg-black/5 dark:border-white/15 dark:hover:bg-white/10"
						>
							Hubungi Saya
						</a>
					</div>
				</div>

				<div class="flex gap-10 lg:gap-16">
					<div>
						<p class="text-4xl font-black tracking-tight lg:text-5xl">03+</p>
						<p class="mt-2 text-xs text-gray-400">Project Experience</p>
					</div>

					<div>
						<p class="text-4xl font-black tracking-tight lg:text-5xl">PPLG</p>
						<p class="mt-2 text-xs text-gray-400">My Major</p>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- IMAGE BANNER -->
	<section class="mx-auto max-w-[1400px] px-6 lg:px-16">
		<div class="group relative overflow-hidden rounded-[28px]">
			<img
				src="/images/langit.jpg"
				alt="Foto kegiatan lab RPL"
				class="h-[260px] w-full object-cover transition duration-700 group-hover:scale-[1.03] lg:h-[480px]"
			/>

			<div
				class="absolute inset-0 bg-gradient-to-t from-black/70 via-transparent to-transparent"
			></div>

			<div
				class="absolute bottom-0 left-0 flex w-full flex-col justify-between gap-3 p-6 text-white sm:flex-row sm:items-end sm:p-10"
			>
				<div>
					<p class="mb-2 text-[10px] font-semibold tracking-[3px] text-orange-300">
						BEHIND THE SCENES
					</p>
					<h2 class="text-2xl font-bold lg:text-4xl">Learning by Creating.</h2>
				</div>

				<p class="text-xs tracking-widest text-white/70">LAB RPL — 2026</p>
			</div>
		</div>
	</section>

	<!-- PROJECTS -->
	<section
		id="proyek"
		class="mx-auto max-w-[1400px] px-6 py-28 transition-colors duration-300 lg:px-16 lg:py-36"
	>
		<div class="mb-12 flex flex-col justify-between gap-5 md:flex-row md:items-end">
			<div>
				<p class="mb-4 text-xs font-bold tracking-[3px] text-[#ff7043]">
					01 / SELECTED WORKS
				</p>

				<h2 class="text-4xl font-black tracking-tight sm:text-5xl lg:text-6xl">
					My Projects<span class="text-[#ff7043]">.</span>
				</h2>
			</div>

			<p class="max-w-[350px] text-sm leading-relaxed text-gray-500 dark:text-gray-400">
				Beberapa proyek yang saya kerjakan sebagai bagian dari proses belajar dan eksplorasi
				teknologi.
			</p>
		</div>

		<div
			class="overflow-hidden rounded-[24px] border border-black/5 bg-white px-5 transition-colors duration-300 dark:border-white/10 dark:bg-[#1d1d1d] sm:px-9"
		>
			{#each projects as project, i (project.title)}
				<div class="transition duration-300 hover:translate-x-1">
					<ProjectRow {project} index={i} />
				</div>
			{/each}
		</div>
	</section>

	<!-- ABOUT -->
	<section
		id="tentang"
		class="border-y border-black/5 bg-[#f1eee8] py-24 transition-colors duration-300 dark:border-white/10 dark:bg-[#1b1b1b] lg:py-32"
	>
		<div class="mx-auto max-w-[1400px] px-6 lg:px-16">
			<div class="mb-14">
				<p class="mb-4 text-xs font-bold tracking-[3px] text-[#ff7043]">
					02 / GET TO KNOW ME
				</p>

				<h2 class="text-4xl font-black tracking-tight sm:text-5xl lg:text-6xl">
					About Me<span class="text-[#ff7043]">.</span>
				</h2>
			</div>

			<div class="grid items-center gap-12 lg:grid-cols-2 lg:gap-20">
				<div class="relative">
					<div
						class="absolute -left-4 -top-4 h-24 w-24 rounded-tl-[25px] border-l-4 border-t-4 border-[#ff7043]"
					></div>

					<img
						src="/images/arrietty.jpg"
						alt="Foto profil"
						class="relative z-10 h-[400px] w-full rounded-[24px] object-cover shadow-xl lg:h-[570px]"
					/>

					<div
						class="absolute -bottom-5 -right-4 z-20 rounded-2xl bg-[#ff7043] px-6 py-4 text-white shadow-xl"
					>
						<p class="text-xs font-medium tracking-widest">BASED IN</p>
						<p class="mt-1 text-lg font-bold">Indonesia 🇮🇩</p>
					</div>
				</div>

				<div>
					<h3 class="mb-6 text-2xl font-bold leading-snug lg:text-3xl">
						Exploring technology, creating ideas, and building something meaningful.
					</h3>

					<p class="mb-10 text-base leading-[1.9] text-gray-500 dark:text-gray-400">
						{profile.bio}
					</p>

					<div class="mb-10 divide-y divide-black/10 dark:divide-white/10">
						{#each profile.facts as fact}
							<div class="flex items-center justify-between gap-5 py-5">
								<span class="text-xs font-bold tracking-widest text-gray-400">
									{fact.label}
								</span>

								<span class="text-right text-sm font-semibold">
									{fact.value}
								</span>
							</div>
						{/each}
					</div>

					<div>
						<p class="mb-5 text-xs font-bold tracking-[3px] text-[#ff7043]">
							TOOLS & SKILLS
						</p>

						<div class="flex flex-wrap gap-3">
							{#each profile.skills as skill}
								<span
									class="rounded-full border border-black/10 bg-white px-5 py-3 text-xs font-medium transition hover:border-[#ff7043] hover:text-[#ff7043] dark:border-white/10 dark:bg-[#242424]"
								>
									{skill}
								</span>
							{/each}
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- CONTACT -->
	<section
		id="kontak"
		class="mx-auto max-w-[1400px] px-6 py-28 transition-colors duration-300 lg:px-16 lg:py-36"
	>
		<div class="mb-14">
			<p class="mb-4 text-xs font-bold tracking-[3px] text-[#ff7043]">
				03 / LET'S CONNECT
			</p>

			<h2
				class="max-w-[850px] text-5xl font-black leading-[1.05] tracking-tight sm:text-6xl lg:text-8xl"
			>
				Let's Talk
				<span class="text-[#ff7043]">Together.</span>
			</h2>
		</div>

		<div class="grid gap-14 lg:grid-cols-2 lg:gap-24">
			<div>
				<p class="max-w-[430px] text-lg leading-relaxed text-gray-500 dark:text-gray-400">
					Punya pertanyaan, ide menarik, atau ingin berdiskusi? Saya akan senang mendengar
					pesan dari kamu.
				</p>

				<div class="mt-12">
					<p class="mb-3 text-xs font-bold tracking-[2px] text-gray-400">
						GET IN TOUCH
					</p>

					<a
						href="mailto:oliviaokta@gmail.com"
						class="inline-flex items-center gap-3 text-lg font-bold transition hover:text-[#ff7043]"
					>
						oliviaokta@gmail.com

						<svg
							width="18"
							height="18"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="1.7"
						>
							<path d="M7 17 17 7M7 7h10v10" />
						</svg>
					</a>
				</div>
			</div>

			<form
				method="POST"
				action="?/kirim"
				use:enhance={() => {
					status = 'loading';

					return async ({ result, update }) => {
						await update({ reset: result.type === 'success' });

						status = result.type === 'success' ? 'success' : 'error';
					};
				}}
				class="flex flex-col gap-6"
			>
				<label class="flex flex-col gap-3">
					<span class="text-xs font-bold tracking-widest text-gray-400">
						YOUR NAME
					</span>

					<input
						name="nama"
						required
						autocomplete="name"
						placeholder="Masukkan nama kamu"
						class="h-14 w-full rounded-xl border border-black/10 bg-white px-5 text-sm outline-none transition placeholder:text-gray-400 focus:border-[#ff7043] focus:ring-2 focus:ring-[#ff7043]/10 dark:border-white/10 dark:bg-[#202020] dark:text-white"
					/>
				</label>

				<label class="flex flex-col gap-3">
					<span class="text-xs font-bold tracking-widest text-gray-400">
						EMAIL ADDRESS
					</span>

					<input
						name="email"
						type="email"
						required
						autocomplete="email"
						placeholder="nama@gmail.com"
						class="h-14 w-full rounded-xl border border-black/10 bg-white px-5 text-sm outline-none transition placeholder:text-gray-400 focus:border-[#ff7043] focus:ring-2 focus:ring-[#ff7043]/10 dark:border-white/10 dark:bg-[#202020] dark:text-white"
					/>
				</label>

				<label class="flex flex-col gap-3">
					<span class="text-xs font-bold tracking-widest text-gray-400">
						YOUR MESSAGE
					</span>

					<textarea
						name="pesan"
						required
						rows="5"
						placeholder="Ceritakan sesuatu..."
						class="min-h-[150px] w-full resize-y rounded-xl border border-black/10 bg-white px-5 py-4 text-sm outline-none transition placeholder:text-gray-400 focus:border-[#ff7043] focus:ring-2 focus:ring-[#ff7043]/10 dark:border-white/10 dark:bg-[#202020] dark:text-white"
					></textarea>
				</label>

				<button
					type="submit"
					disabled={status === 'loading'}
					class="flex h-14 items-center justify-center gap-3 rounded-xl bg-[#ff7043] text-sm font-bold text-white shadow-lg shadow-[#ff7043]/20 transition hover:-translate-y-1 hover:bg-[#ed5e32] disabled:cursor-not-allowed disabled:opacity-60"
				>
					{#if status === 'loading'}
						<svg
							width="18"
							height="18"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
							class="animate-spin"
						>
							<path d="M12 3a9 9 0 1 0 9 9" />
						</svg>
						Mengirim pesan...
					{:else}
						Kirim Pesan

						<svg
							width="18"
							height="18"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
						>
							<path d="M5 12h14m-7-7 7 7-7 7" />
						</svg>
					{/if}
				</button>

				{#if status === 'success'}
					<div
						class="rounded-xl border border-green-500/20 bg-green-500/10 p-4 text-sm text-green-600"
					>
						✓ Pesan berhasil dikirim. Terima kasih!
					</div>
				{:else if status === 'error'}
					<div
						class="rounded-xl border border-red-500/20 bg-red-500/10 p-4 text-sm text-red-500"
					>
						✕ Gagal mengirim pesan. Silakan coba lagi.
					</div>
				{/if}
			</form>
		</div>
	</section>

	<!-- FOOTER -->
	<footer class="bg-[#242424] text-white">
		<div class="mx-auto max-w-[1400px] px-6 py-16 lg:px-16 lg:py-20">
			<div class="flex flex-col justify-between gap-12 lg:flex-row lg:items-end">
				<div>
					<p class="mb-5 text-xs font-bold tracking-[3px] text-[#ff7043]">
						THANK YOU FOR VISITING
					</p>

					<h2
						class="max-w-[600px] text-5xl font-black leading-tight tracking-tight lg:text-7xl"
					>
						Keep Learning.
						<br />
						<span class="text-[#ff7043]">Keep Creating.</span>
					</h2>
				</div>

				<div class="flex flex-col gap-5">
					<p class="text-xs tracking-widest text-gray-400">LET'S CONNECT</p>

					<a
						href="mailto:oliviaokta@gmail.com"
						class="text-lg font-semibold transition hover:text-[#ff7043]"
					>
						oliviaokta@gmail.com
					</a>

					<a
						href="https://github.com/nama-kamu"
						target="_blank"
						rel="noopener noreferrer"
						class="text-sm text-gray-400 transition hover:text-white"
					>
						GitHub ↗
					</a>
				</div>
			</div>

			<div
				class="mt-20 flex flex-col justify-between gap-5 border-t border-white/10 pt-8 sm:flex-row sm:items-center"
			>
				<p class="text-xs text-gray-500">
					© 2026 Olivia. All rights reserved.
				</p>

				<a
					href="#home"
					class="text-xs font-semibold tracking-widest text-[#ff7043] transition hover:text-white"
				>
					BACK TO TOP ↑
				</a>
			</div>
		</div>
	</footer>
</div>