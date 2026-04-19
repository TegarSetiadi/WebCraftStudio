<script lang="ts">
	import { page } from '$app/state';
	import { SITE } from '$lib/config';

	const is404 = $derived(page.status === 404);
</script>

<svelte:head>
	<title>{is404 ? '404 Halaman Tidak Ditemukan' : `Error ${page.status}`} | {SITE.name}</title>
	<meta name="robots" content="noindex" />
</svelte:head>

<div class="error-page">
	<div class="bg-glow" aria-hidden="true"></div>

	<div class="card">
		{#if is404}
			<div class="code gradient-text">404</div>
			<h1>Halaman Tidak Ditemukan</h1>
			<p>Halaman yang Anda cari tidak ada atau sudah dipindahkan.</p>
		{:else}
			<div class="code gradient-text">{page.status}</div>
			<h1>Terjadi Kesalahan</h1>
			<p>{page.error?.message ?? 'Terjadi kesalahan yang tidak terduga.'}</p>
		{/if}

		<div class="actions">
			<a href="/" class="btn-primary">← Kembali ke Beranda</a>
			<a
				href="https://wa.me/{SITE.whatsapp}"
				target="_blank" rel="noopener noreferrer"
				class="btn-ghost"
			>💬 Laporkan Masalah</a>
		</div>
	</div>
</div>

<style>
	:global(body) { background: #06060f; }
	.error-page {
		min-height: 100vh; display: flex; align-items: center; justify-content: center;
		background: #06060f; position: relative; overflow: hidden; padding: 2rem;
		font-family: 'Inter', system-ui, sans-serif;
	}
	.bg-glow {
		position: absolute; top: 30%; left: 50%; transform: translate(-50%, -50%);
		width: 600px; height: 400px; pointer-events: none;
		background: radial-gradient(ellipse, rgba(124,58,237,0.18) 0%, transparent 70%);
	}
	.card {
		position: relative; z-index: 2; text-align: center; max-width: 520px;
		background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.08);
		border-radius: 1.75rem; padding: 3.5rem 2.5rem;
	}
	.code {
		font-size: clamp(5rem, 15vw, 9rem); font-weight: 900; line-height: 1;
		margin-bottom: 1rem; letter-spacing: -0.04em;
	}
	.gradient-text {
		background: linear-gradient(135deg, #a78bfa, #38bdf8);
		-webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
	}
	h1 { font-size: 1.6rem; font-weight: 800; color: #f1f5f9; margin-bottom: 0.75rem; }
	p { color: #64748b; font-size: 0.95rem; line-height: 1.65; margin-bottom: 2rem; }
	.actions { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; }
	.btn-primary {
		background: linear-gradient(135deg, #7c3aed, #4f46e5); color: #fff;
		padding: 0.75rem 1.75rem; border-radius: 9999px; font-weight: 700;
		font-size: 0.95rem; text-decoration: none;
		box-shadow: 0 8px 24px rgba(124,58,237,0.35);
		transition: transform 0.2s, box-shadow 0.2s;
	}
	.btn-primary:hover { transform: translateY(-2px); box-shadow: 0 12px 32px rgba(124,58,237,0.5); }
	.btn-ghost {
		background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.12);
		color: #e2e8f0; padding: 0.75rem 1.75rem; border-radius: 9999px;
		font-weight: 600; font-size: 0.95rem; text-decoration: none; transition: background 0.2s;
	}
	.btn-ghost:hover { background: rgba(255,255,255,0.09); }
</style>
