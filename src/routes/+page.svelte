<script lang="ts">
	import { onMount } from 'svelte';
	import { SITE } from '$lib/config';
	import Navbar from '$lib/components/Navbar.svelte';
	import Hero from '$lib/components/Hero.svelte';
	import Services from '$lib/components/Services.svelte';
	import Process from '$lib/components/Process.svelte';
	import Testimonials from '$lib/components/Testimonials.svelte';
	import FAQ from '$lib/components/FAQ.svelte';
	import Contact from '$lib/components/Contact.svelte';
	import Footer from '$lib/components/Footer.svelte';

	let navScrolled = $state(false);
	let heroVisible = $state(false);

	onMount(() => {
		// Trigger hero fade-in
		setTimeout(() => (heroVisible = true), 80);

		// Navbar scroll state
		const onScroll = () => { navScrolled = window.scrollY > 50; };
		window.addEventListener('scroll', onScroll, { passive: true });

		// Reveal sections via IntersectionObserver
		const io = new IntersectionObserver(
			(entries) => entries.forEach((e) => {
				if (e.isIntersecting) {
					(e.target as HTMLElement).style.opacity = '1';
					(e.target as HTMLElement).style.transform = 'translateY(0)';
					io.unobserve(e.target);
				}
			}),
			{ threshold: 0.1, rootMargin: '0px 0px -60px 0px' }
		);
		document.querySelectorAll('.reveal').forEach((el) => io.observe(el));

		return () => {
			window.removeEventListener('scroll', onScroll);
			io.disconnect();
		};
	});
</script>

<svelte:head>
	<title>{SITE.name} | {SITE.tagline}</title>
	<meta name="description" content={SITE.description} />
	<meta name="keywords" content="jasa buat website, jasa web murah, landing page, toko online, company profile, web developer Indonesia" />
	<meta name="robots" content="index, follow" />
	<link rel="canonical" href={SITE.url} />

	<meta property="og:type" content="website" />
	<meta property="og:url" content={SITE.url} />
	<meta property="og:title" content="{SITE.name} | {SITE.tagline}" />
	<meta property="og:description" content={SITE.description} />
	<meta property="og:locale" content="id_ID" />

	<meta name="twitter:card" content="summary_large_image" />
	<meta name="twitter:title" content="{SITE.name} | Jasa Website Profesional" />
	<meta name="twitter:description" content={SITE.description} />

	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap" rel="stylesheet" />

	{@html `<script type="application/ld+json">${JSON.stringify({
		"@context": "https://schema.org",
		"@type": "ProfessionalService",
		"name": SITE.name,
		"url": SITE.url,
		"description": SITE.description,
		"areaServed": "ID",
		"telephone": "+" + SITE.whatsapp,
		"priceRange": "Rp 200.000 - Rp 5.000.000",
		"aggregateRating": { "@type": "AggregateRating", "ratingValue": "4.9", "reviewCount": "50" }
	})}</script>`}
</svelte:head>

<Navbar scrolled={navScrolled} />
<Hero visible={heroVisible} />
<Services />
<Process />
<Testimonials />
<FAQ />
<Contact />
<Footer />

<style>
	:global(*, *::before, *::after) { box-sizing: border-box; margin: 0; padding: 0; }
	:global(html) { scroll-behavior: smooth; }
	:global(body) {
		font-family: 'Inter', system-ui, sans-serif;
		background: #06060f; color: #e2e8f0;
		overflow-x: hidden; -webkit-font-smoothing: antialiased;
	}
	:global(.reveal) {
		opacity: 0; transform: translateY(24px);
		transition: opacity 0.6s ease, transform 0.6s ease;
		will-change: opacity, transform;
	}
	@media (prefers-reduced-motion: reduce) {
		:global(.reveal) { transition: none; opacity: 1; transform: none; }
	}
</style>