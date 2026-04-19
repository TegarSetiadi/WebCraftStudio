<script lang="ts">
	import { SITE } from '$lib/config';
</script>

<footer class="footer">
	<div class="container footer-inner">
		<div class="logo">
			<span aria-hidden="true">⚡</span>
			<span>WebCraft<strong>Studio</strong></span>
		</div>
		<p class="footer-copy">© {new Date().getFullYear()} {SITE.name}. Dibuat dengan ❤️ di Indonesia.</p>
		<nav class="footer-links" aria-label="Footer navigasi">
			<a href="#services">Layanan</a>
			<a href="#contact">Kontak</a>
		</nav>
	</div>
</footer>

<style>
	.footer { background: #06060f; border-top: 1px solid rgba(255,255,255,0.06); padding: 2rem 1.5rem; }
	.container { max-width: 1200px; margin: 0 auto; }
	.footer-inner { display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 1rem; }
	.logo { display: flex; align-items: center; gap: 0.5rem; font-size: 1.1rem; color: #e2e8f0; font-weight: 600; }
	.logo strong { color: #a78bfa; }
	.footer-copy { color: #475569; font-size: 0.8rem; }
	.footer-links { display: flex; gap: 1.5rem; }
	.footer-links a { color: #475569; font-size: 0.8rem; text-decoration: none; transition: color 0.2s; }
	.footer-links a:hover { color: #a78bfa; }
	@media (max-width: 640px) { .footer-inner { flex-direction: column; text-align: center; } }
</style>
