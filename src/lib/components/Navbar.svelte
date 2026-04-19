<script lang="ts">
	import { SITE } from '$lib/config';

	let { scrolled = false }: { scrolled: boolean } = $props();
</script>

<nav class="navbar" class:scrolled aria-label="Navigasi utama">
	<div class="nav-inner">
		<a href="#hero" class="logo" aria-label="{SITE.name} - Beranda">
			<span aria-hidden="true">⚡</span>
			<span>WebCraft<strong>Studio</strong></span>
		</a>
		<div class="nav-links">
			<a href="#services">Layanan</a>
			<a href="#process">Proses</a>
			<a href="#testimonials">Testimoni</a>
			<a href="#faq">FAQ</a>
			<a href="#contact" id="nav-cta-btn" class="btn-nav">Hubungi Kami</a>
		</div>
	</div>
</nav>

<style>
	.navbar {
		position: fixed; top: 0; left: 0; right: 0; z-index: 100;
		padding: 1.25rem 2rem;
		transition: background 0.3s, padding 0.3s, border-color 0.3s;
	}
	.navbar.scrolled {
		background: rgba(6, 6, 15, 0.88);
		backdrop-filter: blur(18px);
		-webkit-backdrop-filter: blur(18px);
		border-bottom: 1px solid rgba(139, 92, 246, 0.2);
		padding: 0.75rem 2rem;
	}
	.nav-inner {
		max-width: 1200px; margin: 0 auto;
		display: flex; align-items: center; justify-content: space-between;
	}
	.logo {
		display: flex; align-items: center; gap: 0.5rem;
		font-size: 1.1rem; color: #e2e8f0; text-decoration: none; font-weight: 600;
	}
	.logo strong { color: #a78bfa; }
	.nav-links { display: flex; align-items: center; gap: 2rem; }
	.nav-links a {
		color: #94a3b8; text-decoration: none; font-size: 0.875rem; font-weight: 500;
		transition: color 0.2s;
	}
	.nav-links a:hover { color: #f1f5f9; }
	.btn-nav {
		background: linear-gradient(135deg, #7c3aed, #4f46e5);
		color: #fff !important; padding: 0.5rem 1.2rem; border-radius: 9999px;
		font-size: 0.85rem !important;
		transition: transform 0.2s, box-shadow 0.2s;
	}
	.btn-nav:hover { transform: translateY(-1px); box-shadow: 0 6px 20px rgba(124, 58, 237, 0.4); }

	@media (max-width: 640px) { .nav-links { display: none; } }
</style>
