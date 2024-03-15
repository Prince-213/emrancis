<script lang="ts">
	import { gsap } from 'gsap';

	import { ScrollTrigger } from 'gsap/dist/ScrollTrigger';

	import anime from '$lib/anime/anime.min.js';

	import '$lib/assets/blobz.min.css';

	import guy from '$lib/assets/3d-casual-life-young-man-surrounded-by-gadgets-writing-notes.png';

	import { browser } from '$app/environment';

	import { Button } from '$lib/components/ui/button';

	import imagesLoaded from 'imagesloaded';

	import {
		ArrowTopRight,
		Pause,
		NotionLogo,
		TwitterLogo,
		VercelLogo,
		GithubLogo,
		FigmaLogo,
		DiscordLogo,
		IconjarLogo,
		ChevronLeft,
		ChevronRight,
		CheckCircled
	} from 'svelte-radix';
	import Lenis from '@studio-freight/lenis';

	import { onMount } from 'svelte';

	const projects = [
		'florian-olivo-4hbJ-eymZ1o-unsplash.jpg',
		'tech-doodle.jpg',
		'markus-spiske-iar-afB0QQw-unsplash.jpg',
		'html-system-website-concept.jpg',
		'vecteezy_simple-childish-scribble-backdrop-colorful-doodle-art_8362482.jpg'
	];

	import SplitType from 'split-type';

	gsap.registerPlugin(ScrollTrigger);

	const services = [
		{
			name: 'Branding',
			icon: 'icons8-cloth-94.png'
		},
		{
			name: 'Interactive-Design',
			icon: 'icons8-tv-94.png'
		},
		{
			name: 'Programming',
			icon: 'icons8-github-94.png'
		},
		{
			name: 'Graphics',
			icon: 'icons8-paint-100.png'
		},
		{
			name: 'SEO',
			icon: '3d-rocket.png'
		},
		{
			name: 'Photography',
			icon: 'icons8-camera-100.png'
		}
	];

	let loaded = false;

	onMount(() => {
		const lenis = new Lenis({
			duration: 1,
			easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t))
		});

		function raf(time) {
			lenis.raf(time);
			requestAnimationFrame(raf);
		}

		requestAnimationFrame(raf);

		const ourText = SplitType.create('.heading', { types: 'chars' });
		const chars = ourText.chars;

		const ourServices = SplitType.create('.services', { types: 'chars' });

		const servTime = gsap.timeline();

		var morphing = anime({
			targets: '#morphing .p',
			d: [
				{
					value:
						'M171.5,-191.9C215.3,-167.6,239.1,-107,234.1,-53.5C229,0.1,195,46.5,157.5,71.5C119.9,96.5,78.8,99.9,37.7,123.4C-3.3,146.9,-44.2,190.4,-72.4,185.9C-100.7,181.3,-116.1,128.7,-133.1,84.2C-150.1,39.7,-168.6,3.3,-177.6,-46.2C-186.7,-95.8,-186.2,-158.6,-155,-185.1C-123.8,-211.6,-61.9,-201.8,1,-202.9C63.9,-204.1,127.7,-216.2,171.5,-191.9Z'
				},
				{
					value:
						'M95,-109.2C143.2,-72.7,216.4,-61.9,232.3,-32C248.2,-2.2,206.8,46.6,170.7,88.7C134.7,130.7,103.9,165.9,67.2,175C30.6,184.2,-12.1,167.3,-52.4,150C-92.8,132.7,-130.8,115.1,-141.6,86.6C-152.3,58,-135.7,18.5,-134,-29.3C-132.4,-77.1,-145.6,-133.1,-125.7,-174.6C-105.8,-216.1,-52.9,-243.1,-14.8,-225.5C23.4,-207.8,46.7,-145.7,95,-109.2Z'
				}
			],
			easing: 'easeInOutSine',
			duration: 6000,
			direction: 'infinite alternate',
			loop: true
		});

		gsap.from('#title', {
			opacity: 0,
			duration: 1,
			ease: 'power1.out',
			y: 100,
			delay: 1
		});

		gsap.from(chars, {
			y: 50,
			stagger: 0.1,
			ease: 'power4.out'
		});

		gsap.from(ourServices.chars, {
			y: 95,
			stagger: 0.05,
			ease: 'power4.out',
			scrollTrigger: {
				trigger: '.services',
				scrub: 1
			},
			duration: 0.5
		});

		gsap.from('.boxesleft', {
			x: -100,
			opacity: 0,
			delay: 0.6,
			stagger: 0.3,
			scrollTrigger: {
				trigger: '.boxesleft'
			}
		});

		gsap.from('.boxesright', {
			x: 100,
			opacity: 0,
			delay: 0.6,
			stagger: 0.3,
			scrollTrigger: {
				trigger: '.boxesright'
			}
		});

		const tl = gsap.timeline();
		const line = gsap.timeline({ repeat: -1 });

		let md = gsap.matchMedia();

		md.add('(min-width: 600px)', () => {
			const photos = gsap.utils.toArray('.featuredPhoto:not(:first-child)');
			const details = gsap.utils.toArray('.desktopContent:not(:first-child)');

			gsap.set(photos, { yPercent: 140, opacity: 0 });

			const animation = gsap.to(photos, {
				yPercent: 0,
				opacity: 1,
				ease: 'power4.out',
				duration: 1,
				stagger: 1
			});

			let st = ScrollTrigger.create({
				trigger: '.gallery',
				pin: '.pin',
				start: 'top top',
				end: 'bottom bottom',

				scrub: 1,
				animation: animation,
				markers: false
			});

			details.forEach((detail: any, index: any) => {
				let headline = detail.querySelector('h1');

				ScrollTrigger.create({
					trigger: headline,

					start: 'top 30%',
					end: 'top 60%',

					animation: gsap.to(photos[index], { yPercent: 0, opacity: 1, ease: 'power4.out' }),
					scrub: true,
					markers: false
				});
			});

			console.log(st.pin);
		});

		tl.from('.logo', {
			opacity: 0,
			y: 10,
			ease: 'back.in',
			duration: 1,
			delay: 0.5
		}).from('nav p', {
			y: 50,
			ease: 'back.inOut',
			opacity: 0,
			duration: 0.8,
			stagger: 0.2
		});
	});

	let billing = 'month';

	import budget from '$lib/assets/casual-life-3d-girl-planning-budget-with-tablet-and-piggy-bank.png';
</script>

<div class=" scrollbar1 relative w-full overflow-x-hidden font-jose" id="fullpage">
	<!-- <div class="blob right-0 top-[100vh] z-40"></div> -->
	<div class=" line h-[10px] w-full"></div>
	<div class=" absolute left-[1rem] top-[12rem] h-3 w-3 rounded-[50%] bg-[#48d7c6]"></div>
	<div class=" absolute left-[6rem] top-[21rem] h-5 w-5 rounded-[50%] bg-[#f33e21]"></div>
	<div class=" absolute left-[1.2rem] top-[44rem] h-2 w-2 rounded-[50%] bg-[#8b9595e2]"></div>

	<div class=" absolute right-[15rem] top-[16rem] h-3 w-3 rounded-[50%] bg-[#48d7c6]"></div>
	<div class=" absolute right-[13rem] top-[28rem] h-2 w-2 rounded-[50%] bg-[#f33e21]"></div>
	<div class=" absolute right-[44rem] top-[45rem] h-7 w-7 rounded-[50%] bg-[#f33e21]"></div>

	<svg
		class="blob -right-[4rem] top-[60vh] -z-40 md:right-0"
		id="morphing"
		xmlns="http://www.w3.org/2000/svg"
		width="800"
		height="800"
		viewBox="0 0 400 400"
	>
		<defs>
			<linearGradient id="grad1" x1="0%" y1="0%" x2="100%" y2="0%">
				<stop offset="0%" style="stop-color:#30DE5084;stop-opacity:1" />

				<stop offset="100%" style="stop-color:#ED0F0F82;stop-opacity:1" />
			</linearGradient>
		</defs>
		<g transform="translate(300,300)">
			<path
				class="p"
				d="M95,-109.2C143.2,-72.7,216.4,-61.9,232.3,-32C248.2,-2.2,206.8,46.6,170.7,88.7C134.7,130.7,103.9,165.9,67.2,175C30.6,184.2,-12.1,167.3,-52.4,150C-92.8,132.7,-130.8,115.1,-141.6,86.6C-152.3,58,-135.7,18.5,-134,-29.3C-132.4,-77.1,-145.6,-133.1,-125.7,-174.6C-105.8,-216.1,-52.9,-243.1,-14.8,-225.5C23.4,-207.8,46.7,-145.7,95,-109.2Z"
				fill="url(#grad1)"
			/>
		</g>
	</svg>

	<div
		class=" absolute -right-[1rem] top-[10rem] h-[2.5rem] w-[2.5rem] rounded-[50%] bg-[#faa807]"
	></div>

	<div
		class=" absolute -right-[1rem] top-[22rem] h-[5rem] w-[5rem] rounded-[50%] bg-[#7c7b8133]"
	></div>

	<main class=" images section min-h-[80vh] w-full md:h-screen">
		<header class=" mx-auto w-[75%] pt-6">
			<div class=" flex w-full items-center justify-between">
				<div class=" logo flex w-[30%] items-end space-x-1">
					<img width="40px" src="./mocklogo.png" alt="" />
					<h1 class=" text-5xl font-semibold">zuma</h1>
				</div>

				<nav class=" hidden h-[4rem] items-center space-x-10 overflow-y-hidden md:flex">
					<p
						class=" relative cursor-pointer text-[14px] font-bold uppercase after:absolute after:-bottom-[10px] after:left-[50%] after:h-[6px] after:w-[6px] after:-translate-x-[50%] after:rounded-[50%] after:bg-black"
					>
						Home
					</p>
					<p class=" cursor-pointer text-[14px] font-bold uppercase text-gray-400">Cases</p>
					<p class=" cursor-pointer text-[14px] font-bold uppercase text-gray-400">Blog</p>
					<p class=" cursor-pointer text-[14px] font-bold uppercase text-gray-400">Shop</p>
					<p class=" cursor-pointer text-[14px] font-bold uppercase text-gray-400">News</p>
				</nav>

				<div class=" flex items-center space-x-5">
					<button
						class=" hidden items-start rounded-full border-[1px] border-gray-400 px-6 py-2 pb-1 text-[16px] font-bold uppercase text-black shadow-lg duration-100 ease-in-out hover:shadow-inner md:flex"
						><p>GET QUOTE</p>
						<ArrowTopRight size="20" class=" ml-1" /></button
					>
					<button
						class=" rounded-[50%] border-[1px] border-gray-400 p-2 font-bold uppercase text-black shadow-lg duration-100 ease-in-out hover:shadow-inner lg:hidden"
						><Pause class="rotate-90" /></button
					>
				</div>
			</div>
		</header>

		<!-- <section class=" images mx-auto mt-[12vh] hidden w-[70%]">
			<h1 class=" mb-[8vh] text-[18px] font-medium uppercase text-gray-500">zuma digital studio</h1>
			<h1 class=" relative min-w-full text-[20px] md:text-[128px] font-semibold md:leading-[.9em]">
				<div class="  absolute right-[8rem] top-[0rem] h-[80px] w-[120px] rounded-xl bg-[#dedde5]">
					<img
						class=" -translate-y-[20px] translate-x-[15px] rotate-6"
						width="90px"
						src="./icons8-crown-94.png"
						alt=""
					/>
				</div>
				<div
					class="  absolute bottom-0 right-[9.5rem] h-[70px] w-[140px] -translate-x-[14rem] -translate-y-[9rem] rounded-full bg-[#cfcbd1]"
				>
					<img
						class=" -translate-y-[20px] translate-x-[25px] rotate-45"
						width="100px"
						src="./3d-rocket.png"
						alt=""
					/>
				</div>
				<div
					class="  absolute bottom-0 left-0 h-[70px] w-[160px] -translate-x-[0rem] -translate-y-[1rem] rounded-full bg-[#cfcbd1]"
				>
					<img
						class=" -translate-y-[20px] translate-x-[25px] rotate-45"
						width="100px"
						src="./3d-target.png"
						alt=""
					/>
				</div>
				we help brands<span class=" px-20"></span> with
				<span
					class=" relative z-50 before:absolute before:bottom-[20%] before:left-0 before:-z-20 before:h-10 before:w-full before:bg-gradient-to-r before:from-[#fcbc41] before:to-transparent"
					>compelling</span
				> <span class=" font-satisfy font-thin">and</span>
				<span
					class=" relative z-50 before:absolute before:bottom-[20%] before:left-0 before:-z-20 before:h-10 before:w-full before:bg-gradient-to-r before:from-[#fcbc41] before:to-transparent"
					>persuasive</span
				> <span class=" px-40"></span> <span class=" ml-[12rem]">design</span>
			</h1>
		</section> -->

		<section class=" mx-auto mt-[6vh] w-[90%] text-center md:mt-[12vh] md:w-[75%]">
			<h1 class=" heading mb-[4vh] text-[18px] font-medium uppercase text-gray-500 md:mb-[8vh]">
				zuma digital studio
			</h1>
			<div class=" flex flex-col items-center justify-center md:hidden">
				<h1 class="text-pretty text-center text-[32px] font-bold leading-[1.4em] md:text-[74px]">
					Unleash your potential craft and personalize
				</h1>
				<div class=" flex w-fit -space-x-4 rtl:space-x-reverse">
					<div
						class="h-[4rem] w-[4rem] rounded-2xl border-2 border-white bg-cover bg-center dark:border-gray-800"
						style="background-image: url(pexels-arianna-jadé-4006576.jpg);"
					/>
					<div
						class="h-[4rem] w-[4rem] rounded-2xl border-2 border-white bg-cover bg-center dark:border-gray-800"
						style="background-image: url(pexels-christina-morillo-1181424.jpg);"
					/>
					<div
						class="h-[4rem] w-[4rem] rounded-2xl border-2 border-white bg-cover bg-center dark:border-gray-800"
						style="background-image: url(pexels-jimmy-jimmy-1484806.jpg);"
					/>
				</div>
				<h1 class="text-pretty text-center text-[32px] font-bold leading-[1.4em] md:text-[74px]">
					your journey. Code Create Customize
				</h1>
			</div>

			<h1
				id="title"
				class=" relative hidden min-w-full text-pretty text-center text-[32px] font-bold leading-[1.4em] md:block md:text-[74px]"
			>
				<!-- <div class="absolute left-[41.5%] top-[38%] flex -space-x-4 rtl:space-x-reverse">
					<div
						class="h-[4rem] w-[4rem] rounded-2xl border-2 border-white bg-cover bg-center dark:border-gray-800"
						style="background-image: url(pexels-arianna-jadé-4006576.jpg);"
					/>
					<div
						class="h-[4rem] w-[4rem] rounded-2xl border-2 border-white bg-cover bg-center dark:border-gray-800"
						style="background-image: url(pexels-christina-morillo-1181424.jpg);"
					/>
					<div
						class="h-[4rem] w-[4rem] rounded-2xl border-2 border-white bg-cover bg-center dark:border-gray-800"
						style="background-image: url(pexels-jimmy-jimmy-1484806.jpg);"
					/>
				</div> -->

				<!-- <div class="  absolute right-[8rem] top-[0rem] h-[80px] w-[120px] rounded-xl bg-[#dedde5]">
					<img
						class=" -translate-y-[20px] translate-x-[15px] rotate-6"
						width="90px"
						src="./icons8-crown-94.png"
						alt=""
					/>
				</div>
				<div
					class="  absolute bottom-0 right-[9.5rem] h-[70px] w-[140px] -translate-x-[14rem] -translate-y-[9rem] rounded-full bg-[#cfcbd1]"
				>
					<img
						class=" -translate-y-[20px] translate-x-[25px] rotate-45"
						width="100px"
						src="./3d-rocket.png"
						alt=""
					/>
				</div>
				<div
					class="  absolute bottom-0 left-0 h-[70px] w-[160px] -translate-x-[0rem] -translate-y-[1rem] rounded-full bg-[#cfcbd1]"
				>
					<img
						class=" -translate-y-[20px] translate-x-[25px] rotate-45"
						width="100px"
						src="./3d-target.png"
						alt=""
					/>
				</div> -->
				Unleash your potential craft and personalize
				<span class=" md:px-[5.2rem]"
					><div class="absolute left-[41.5%] top-[38%] flex -space-x-4 rtl:space-x-reverse">
						<div
							class="h-[4rem] w-[4rem] rounded-2xl border-2 border-white bg-cover bg-center dark:border-gray-800"
							style="background-image: url(pexels-arianna-jadé-4006576.jpg);"
						/>
						<div
							class="h-[4rem] w-[4rem] rounded-2xl border-2 border-white bg-cover bg-center dark:border-gray-800"
							style="background-image: url(pexels-christina-morillo-1181424.jpg);"
						/>
						<div
							class="h-[4rem] w-[4rem] rounded-2xl border-2 border-white bg-cover bg-center dark:border-gray-800"
							style="background-image: url(pexels-jimmy-jimmy-1484806.jpg);"
						/>
					</div>
				</span>
				your journey. <span class=" ">Code</span>
				<span class=" px-[3.5rem]"
					><div
						class=" absolute left-[27.5%] top-[63%] h-[3.6rem] w-[10rem] rounded-xl bg-cover bg-center"
					>
						<img width="120px" src="icons8-code-96.png" alt="" />
					</div></span
				> Create Customize
			</h1>
			<h1
				class=" flex items-center justify-center gap-x-5 text-center text-[32px] font-bold md:text-[74px]"
			>
				Get
				<button
					class="  button-54 flex items-center px-1 transition-all delay-75 duration-150 md:px-4"
				>
					<p class=" text-[12px] md:text-lg">Learn More</p>
				</button>
				started
			</h1>
		</section>
	</main>
	<div
		class=" section relative -z-10 mt-[3.5vh] flex h-screen w-full flex-col justify-between bg-gradient-to-b from-white to-[#d9d9e3] to-90% pb-10 md:pb-0 md:pt-6"
	>
		<div
			class=" z-50 mx-auto flex w-[80%] flex-col items-center justify-center md:w-[70%] md:flex-row md:justify-between"
		>
			<div
				class=" h-[10em] w-[10em] rounded-[50%] bg-gradient-to-r from-orange-700 to-orange-400 md:h-[15em] md:w-[15em]"
			></div>
			<div class=" relative z-50 mt-10 bg-transparent md:mt-0 md:w-[60%]">
				<h1 class=" bg-transparent text-[30px] font-[700] uppercase md:text-[40px]">
					good design mean that good business
				</h1>
				<p class=" mb-[4em] mt-[2em] text-xl font-[400] text-gray-700 md:text-2xl">
					We help our clients succeed by creating identities, digital experiences and printmaterials
					that communicate clearly, acheive community goals and look fantastic
				</p>
				<button
					class=" z-50 flex cursor-pointer items-start rounded-full border-[1px] border-[#29292b] bg-[#29292b] px-[2.2em] py-[1.2em] text-[17px] font-semibold uppercase text-white"
					>ABOUT US
					<ArrowTopRight size="24" class=" ml-1" /></button
				>
			</div>
		</div>
		<div
			class=" mt-10 flex w-full items-center justify-center border-b-[1px] border-t-[1px] border-gray-400 py-[2rem] md:mt-0 md:py-[4rem]"
		>
			<div class=" mx-auto flex w-[90%] items-center justify-between">
				<GithubLogo class=" opacity-70" />
				<FigmaLogo class=" opacity-70" />
				<TwitterLogo class=" opacity-70" />
				<NotionLogo class=" opacity-70" />
				<VercelLogo class=" opacity-70" />
				<DiscordLogo class=" opacity-70" />
				<IconjarLogo class=" opacity-70" />
			</div>
		</div>
	</div>
	<div
		class=" section images flex w-full items-center justify-center bg-[#d9d9e3] py-[4rm] md:min-h-screen md:py-[8rem]"
	>
		<div
			class="  mx-auto grid w-[90%] grid-cols-2 gap-5 rounded-[3rem] bg-cover bg-center py-10 md:h-screen md:grid-cols-4 md:py-0"
		>
			{#each Array(8) as item, idx}
				<div
					style={`background-image: ${idx == 0 || idx == 7 ? 'url(tech-doodle.jpg)' : idx == 4 ? 'url(html-system-website-concept.jpg)' : 'url(vecteezy_simple-childish-scribble-backdrop-colorful-doodle-art_8362482.jpg)'}   ;`}
					class={`card ${idx == 2 ? 'boxesright col-span-2' : ''} ${idx == 0 ? 'boxesleft' : ''}  ${idx == 4 ? 'md:col-span-2' : ''} ${idx == 6 ? 'col-span-2' : ''} ${idx == 3 ? 'boxesleft row-span-2' : ''} ${idx == 7 ? 'boxesright' : ''} ${idx == 5 ? 'boxesright' : ''}   min-h-20 w-full rounded-2xl bg-[#ffffff41] bg-cover bg-center`}
				></div>
			{/each}
		</div>
	</div>
	<div class="  w-full border-b-2 border-gray-300 bg-white pb-[7rem] pt-[8rem]">
		<div class=" mx-auto w-[80%] md:w-[75%]">
			<h1 class=" mb-[3rem] text-[18px] font-medium uppercase text-gray-500">OUR SERVICES</h1>
			<div class=" flex flex-wrap gap-x-[2rem] md:gap-x-[4rem]">
				{#each services as item, idx}
					<div
						class="  relative flex h-fit max-w-fit flex-row items-center overflow-hidden py-0 text-[37px] font-[600] md:text-[76px]"
					>
						<img
							src={item.icon}
							class=" absolute right-[2rem] top-[.5rem] w-[25px] md:w-[45px]"
							alt=""
						/>
						<h1
							class={` services${idx + 1} heading services relative mr-[3rem] bg-gradient-to-r from-[red] to-orange-400 md:mr-[4rem]`}
						>
							{item.name}
						</h1>
						<p class=" font-[300] text-gray-300">/</p>
					</div>
				{/each}
			</div>
		</div>
	</div>
	<div class=" w-full pt-[4rem] md:min-h-fit md:pt-[8rem]">
		<div class="  mx-auto w-[80%] md:w-[70%]">
			<div class=" flex justify-between">
				<h1 class=" mb-[3rem] text-base font-semibold uppercase text-gray-500 md:text-[18px]">
					featured projects
				</h1>
				<h1
					class=" mb-[3rem] flex  items-center text-base font-semibold uppercase text-black md:gap-x-4 md:text-[18px]"
				>
					see all clases <ArrowTopRight />
				</h1>
			</div>
			<div class=" images gallery flex min-h-fit w-full md:mt-0 justify-between">
				<div class=" min-h-screen md:w-[45%]">
					{#each Array(5) as item, idx}
						<div
							style={`border-bottom-width: ${idx == 4 ? '0px' : '0px'}`}
							class=" desktopContent flex h-screen flex-col justify-center border-b-2 pb-[2rem]"
						>
							<h1 class=" text-[34px] font-semibold">Tech Sass Landing Page</h1>
							<p class=" text-balance text-gray-400">
								Branding Lorem ipsum dolor sit amet consectetur adipisicing elit. Rerum delectus
								aut, ipsam assumenda reiciendis molestiae magni beatae tempore? Eum, voluptatibus
								nam totam ad optio mollitia esse odit beatae eveniet? Necessitatibus. Lorem ipsum
								dolor, sit amet consectetur adipisicing elit. Cum, mollitia? Deserunt placeat
								tempore possimus aperiam delectus porro quam adipisci saepe tenetur! Explicabo eos
								adipisci natus ad accusantium ab perferendis accusamus.
							</p>
						</div>
					{/each}
				</div>
				<div class=" pin relative right-0 hidden md:flex h-screen w-[50%] flex-col justify-center">
					<div class=" relative h-[25rem] w-full overflow-hidden rounded-xl">
						{#each Array(5) as item, idx}
							<div
								style={` background-image: url(${projects[idx]})`}
								class=" featuredPhoto md:absolute h-[25rem] w-full rounded-2xl border-2 bg-cover bg-center"
							></div>
						{/each}
					</div>
				</div>
			</div>
		</div>
	</div>
	<div class=" images relative md:min-h-screen w-full overflow-hidden bg-[#ededf5] py-[8rem]">
		<div class=" absolute left-[1rem] top-[12rem] h-3 w-3 rounded-[50%] bg-[#48d7c6]"></div>
		<div class=" absolute left-[6rem] top-[21rem] h-5 w-5 rounded-[50%] bg-[#f33e21]"></div>
		<div class=" absolute left-[1.2rem] top-[44rem] h-2 w-2 rounded-[50%] bg-[#8b9595e2]"></div>
		<img
			src="pexels-arianna-jadé-4006576.jpg"
			class=" absolute -left-[1rem] top-[35rem] md:h-[5rem] md:w-[5rem] w-9 h-9 rounded-[50%] bg-[#8b9595e2]"
			alt=""
		/>

		<img
			src="pexels-jimmy-jimmy-1484806.jpg"
			class=" absolute -top-[1rem] right-[15rem] md:h-[6rem] md:w-[6rem] w-9 h-9 rounded-[50%] bg-[#48d7c6]"
			alt=""
		/>
		<div class=" absolute right-[5rem] top-[24rem] h-6 w-6 rounded-[50%] bg-[#f33e21]"></div>
		<img
			src="pexels-christina-morillo-1181424.jpg"
			alt=""
			class=" absolute -right-[2rem] top-[35rem] md:h-[7rem] md:w-[7rem] w-10 h-10 rounded-[50%] bg-[#f33e21]"
		/>
		<img
			src="pexels-mike-bird-170811.jpg"
			alt=""
			class=" absolute bottom-[3rem] left-[22rem] md:h-[2.5rem] md:w-[2.5rem] w-4 h-4 rounded-[50%] bg-[#f33e21]"
		/>
		<div class=" flex flex-col items-center md:block justify-center mx-auto w-[80%] md:w-[75%]">
			<h1 class=" mb-[8vh] text-[18px] font-medium uppercase text-gray-600">testimonial</h1>
			<div class=" md:flex items-center justify-between">
				<img class=" hidden md:block h-[80vh] w-auto" src={'Man2.png'} alt="" />
				<div class=" md:w-[50%] space-y-10">
					<h1 class=" text-[2.5rem] font-semibold">
						"Zuma studios is 1st our choice for creative services."
					</h1>
					<p class=" text-2xl font-light text-gray-500">
						Lorem ipsum dolor sit amet, consectetur adipisicing elit. Velit fugit ipsam assumenda
						voluptatibus illo repellendus perferendis voluptatum dolorum temporibus. Perspiciatis
						iste ratione cum voluptates omnis mollitia iure nihil repudiandae ex!
					</p>
					<div>
						<h1 class=" text-2xl font-semibold">Nature Jack</h1>
						<p class=" text-balance font-medium text-gray-500">
							Director at <span class=" text-red-500 underline">Newz eMagazine</span>
						</p>
					</div>
					<div class=" flex items-center space-x-5">
						<button
							class=" flex h-[3rem] w-[3rem] items-center justify-center rounded-[50%] bg-white shadow-md"
						>
							<ChevronLeft size="34" />
						</button>
						<button
							class=" flex h-[3rem] w-[3rem] items-center justify-center rounded-[50%] bg-[#121212] text-white shadow-md"
						>
							<ChevronRight size="34" />
						</button>
					</div>
				</div>
			</div>
		</div>
	</div>

	<div class=" min-h-screen w-full bg-white py-[10rem]">
		<div class=" mx-auto flex w-[90%] md:w-[75%] flex-col items-center text-center">
			<h1 class=" mb-[5vh] md:mb-[10vh] text-[18px] font-semibold uppercase text-gray-500">
				choose plan and kick start now
			</h1>
			<div
				class={` relative h-[3rem] md:h-[5rem] transition-all duration-100 ease-out after:absolute after:left-[0.8rem] md:after:left-[1rem] after:z-10 md:after:h-[3.5rem] after:h-[1.8rem] after:w-[45%] after:rounded-full after:bg-white after:transition-all after:duration-100 after:ease-linear ${billing == 'month' ? 'after:translate-x-0 md:after:translate-x-0' : 'md:after:translate-x-[110%] after:translate-x-[100%]'}  mx-auto1 flex w-[90%] md:w-[40%] items-center justify-between rounded-full bg-[#ededf5] px-5 md:px-10 py-3 md:py-6`}
			>
				<button on:click={() => (billing = 'month')} class=" z-40 text-[12px] md:text-lg font-semibold text-black"
					>Front End Dev</button
				>
				<button on:click={() => (billing = 'year')} class=" z-40 text-[12px] md:text-lg font-semibold text-black"
					>Back End Dev <span
						class=" rounded-full hidden md:block bg-gradient-to-r from-orange-600 to-orange-300 px-2 py-1 text-[12px] md:text-lg font-semibold text-white"
						>-15%</span
					></button
				>
			</div>

			<div class=" mb-20 flex w-full justify-between pt-[5rem]">
				<div class=" w-[30%] pb-16 pt-8">
					<div class=" h-[16rem] w-full border-b-[1px] border-gray-500">
						<img class=" w-[150px] md:w-[300px]" src={budget} alt="" />
					</div>

					{#each Array(10) as item, idx}
						<p
							style={` ${idx == 9 ? 'border-width: 0px;' : ''} `}
							class=" flex h-[4rem] items-center border-b-2 text-left text-sm md:text-lg text-gray-600"
						>
							Unlimited Projects
						</p>
					{/each}
				</div>
				<div class=" grid w-[70%] grid-cols-2">
					{#each Array(2) as item, idx}
						<div class={` ${idx == 1 ? 'bg-[#ededf5]' : ''} rounded-xl pb-16 pt-8`}>
							<div
								class={` ${idx == 1 ? ' relative ' : ''} flex h-[16rem] w-full flex-col items-center justify-center space-y-4 border-b-[1px] border-gray-500 pb-10 pt-5`}
							>
								<img
									src="icons8-crown-94.png"
									
									class=" w-[40px] md:w-[80px] absolute -top-[4rem] right-[1rem] rotate-12"
									alt=""
								/>
								<h2 class=" text-sm md:text-lg uppercase">
									{#if idx == 0}
										Basic
									{:else if idx == 1}
										Premium
									
									{/if}
								</h2>
								<h1 class=" text-2xl md:text-7xl font-semibold">$25</h1>
								<p class=" mx-auto max-w-[85%] text-[12px] md:text-base font-normal text-gray-400">
									Journey throuth the basics of Font-End Web Development with a 6 months course !
								</p>
							</div>

							{#each Array(10) as item, idx}
								<p
									style={` ${idx == 9 ? 'border-width: 0px;' : ''} `}
									class=" flex h-[4rem] items-center justify-center border-b-2 text-center text-lg text-green-500"
								>
									<CheckCircled size="20" />
								</p>
							{/each}
							<button
								class={` cursor-pointer items-start rounded-full border-[#29292b] ${idx == 1 ? ' border-0 bg-gradient-to-r from-red-600 to-orange-400 ' : 'bg-[#29292b]'}  mx-auto flex w-[80%] md:w-[60%] justify-center py-[.6rem] md:py-[1.2em] text-[12px] md:text-[16px] font-semibold uppercase text-white shadow-2xl shadow-gray-500 transition-all delay-75 duration-150 ease-in-out hover:shadow-sm `}
								>GET START
								<ArrowTopRight size="20" class=" md:block hidden ml-4" /></button
							>
						</div>
					{/each}
				</div>
			</div>

			<p>
				Didn't find your plan! Are you in need of a tailored plan? <span
					class=" text-lg font-normal text-orange-600">Contact Us</span
				>
			</p>
		</div>
	</div>

	<div class=" min-h-screen w-full border-b-2 border-t-2">
		<div class=" mx-auto flex md:h-screen w-[90%] md:w-[75%] flex-col items-center justify-center">
			<h1 class=" mb-[10vh] text-center text-[18px] font-semibold uppercase text-gray-500">
				professional and friendly is our team
			</h1>
			<div class=" grid w-full gap-y-5 md:gap-y-0 grid-cols-2 md:grid-cols-4">
				{#each Array(4) as item}
					<div class=" flex w-full flex-col items-center justify-center">
						<img src="9439775.jpg" class=" mx-auto h-auto w-[65%] rounded-[50%]" alt="" />
						<div class=" my-[1.5rem] flex flex-col items-center justify-center text-center">
							<h1 class=" text-lg md:text-2xl font-medium">Michal Edwards</h1>
							<p class=" text-gray-400 md:text-lg text-sm">CEO Founder</p>
						</div>
						<div class=" flex items-center space-x-2">
							<div class=" flex h-10 w-10 items-center justify-center rounded-[50%] bg-gray-200">
								<GithubLogo size="14" />
							</div>
							<div class=" flex h-10 w-10 items-center justify-center rounded-[50%] bg-gray-200">
								<TwitterLogo size="14" />
							</div>
						</div>
					</div>
				{/each}
			</div>
			<button
				class={` mx-auto mt-[5rem] flex cursor-pointer items-start justify-center  rounded-full border-[#29292b] bg-[#29292b] px-[2rem] py-[1.2em] text-[16px] font-semibold uppercase text-white shadow-2xl shadow-gray-500 transition-all delay-75 duration-150 ease-in-out hover:shadow-sm `}
			>
				join our team
				<ArrowTopRight size="20" class=" ml-4" /></button
			>
		</div>
	</div>

	<div class=" relative min-h-screen w-full bg-[#ededf5] pb-[8rem] md:pb-[16rem] pt-[4rem] md:pt-[8rem]">
		<!-- <img src="3d-fluency-address-book.png" class=" absolute -bottom-[10rem] -translate-x-[50%] left-[50%]" alt=""> -->
		<div class=" flex w-[90%] mx-auto md:w-full flex-col  items-center justify-center">
			<h1 class=" mb-[10vh] text-[18px] font-semibold uppercase text-gray-500">
				have a project in mind ? connect with us.
			</h1>

			<div class="isolate w-full">
				<form action="#" method="POST" class="mx-auto max-w-xl">
					<div class="grid grid-cols-1 gap-x-8 gap-y-6 sm:grid-cols-2">
						<div>
							<label for="first-name" class="block text-sm font-semibold leading-6 text-gray-900"
								>First name</label
							>
							<div class="mt-2.5">
								<input
									type="text"
									name="first-name"
									id="first-name"
									autocomplete="given-name"
									class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
								/>
							</div>
						</div>
						<div>
							<label for="last-name" class="block text-sm font-semibold leading-6 text-gray-900"
								>Last name</label
							>
							<div class="mt-2.5">
								<input
									type="text"
									name="last-name"
									id="last-name"
									autocomplete="family-name"
									class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
								/>
							</div>
						</div>
						<div class="sm:col-span-2">
							<label for="company" class="block text-sm font-semibold leading-6 text-gray-900"
								>Company</label
							>
							<div class="mt-2.5">
								<input
									type="text"
									name="company"
									id="company"
									autocomplete="organization"
									class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
								/>
							</div>
						</div>
						<div class="sm:col-span-2">
							<label for="email" class="block text-sm font-semibold leading-6 text-gray-900"
								>Email</label
							>
							<div class="mt-2.5">
								<input
									type="email"
									name="email"
									id="email"
									autocomplete="email"
									class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
								/>
							</div>
						</div>
						<div class="sm:col-span-2">
							<label for="phone-number" class="block text-sm font-semibold leading-6 text-gray-900"
								>Phone number</label
							>
							<div class="relative mt-2.5">
								<input
									type="tel"
									name="phone-number"
									id="phone-number"
									autocomplete="tel"
									class="block w-full rounded-md border-0 px-3.5 py-2 pl-20 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
								/>
							</div>
						</div>
						<div class="sm:col-span-2">
							<label for="message" class="block text-sm font-semibold leading-6 text-gray-900"
								>Message</label
							>
							<div class="mt-2.5">
								<textarea
									name="message"
									id="message"
									rows="4"
									class="block w-full rounded-md border-0 px-3.5 py-2 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
								></textarea>
							</div>
						</div>
						<div class="flex gap-x-4 sm:col-span-2">
							<div class="flex h-6 items-center">
								<!-- Enabled: "bg-indigo-600", Not Enabled: "bg-gray-200" -->
								<button
									type="button"
									class="flex w-8 flex-none cursor-pointer rounded-full bg-gray-200 p-px ring-1 ring-inset ring-gray-900/5 transition-colors duration-200 ease-in-out focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
									role="switch"
									aria-checked="false"
									aria-labelledby="switch-1-label"
								>
									<span class="sr-only">Agree to policies</span>
									<!-- Enabled: "translate-x-3.5", Not Enabled: "translate-x-0" -->
									<span
										aria-hidden="true"
										class="h-4 w-4 translate-x-0 transform rounded-full bg-white shadow-sm ring-1 ring-gray-900/5 transition duration-200 ease-in-out"
									></span>
								</button>
							</div>
							<label class="text-sm leading-6 text-gray-600" id="switch-1-label">
								By selecting this, you agree to our
								<a href="#" class="font-semibold text-indigo-600">privacy&nbsp;policy</a>.
							</label>
						</div>
					</div>
					<div class="mt-10">
						<button
							class={` mx-auto flex cursor-pointer items-start justify-center  rounded-full border-[#29292b] bg-[#29292b] px-[2rem] py-[1.2em] text-[16px] font-semibold uppercase text-white shadow-2xl shadow-gray-500 transition-all delay-75 duration-150 ease-in-out hover:shadow-sm `}
						>
							send message
							<ArrowTopRight size="20" class=" ml-4" /></button
						>
					</div>
				</form>
			</div>
		</div>
	</div>
</div>

<style>
	.heading {
		clip-path: polygon(0 0, 100% 0, 100% 100%, 0% 100%);
	}
	.line {
		background: rgb(195, 70, 34);
		background: linear-gradient(
			93deg,
			#dd7f07 0%,
			#c34622 44%,

			#e3f305 76%,
			#31c1b9 100%
		);

		background-size: 220% 220%;
		animation: gradient 15s ease infinite;
	}

	.services {
		-webkit-text-fill-color: transparent;
		-webkit-background-clip: text;
		background-clip: text;
	}

	.card {
		position: relative;
		font-family: 'Open Sans', sans-serif;
		font-size: 16px;
		letter-spacing: 2px;
		text-decoration: none;
		text-transform: uppercase;
		color: #000;
		cursor: pointer;
		border: 3px solid;

		box-shadow:
			1px 1px 0px 0px,
			2px 2px 0px 0px,
			3px 3px 0px 0px,
			4px 4px 0px 0px,
			5px 5px 0px 0px;

		user-select: none;
		-webkit-user-select: none;
		touch-action: manipulation;
	}

	.card:nth-child(1)::before {
		background: radial-gradient(
			800px circle at 400px 400px,
			rgba(154, 137, 114, 0.403),
			transparent 40%
		);
	}

	.button-54 {
		font-family: 'Open Sans', sans-serif;

		letter-spacing: 2px;
		text-decoration: none;
		text-transform: uppercase;
		color: #000;
		cursor: pointer;
		border: 3px solid;

		height: 4.5rem;
		box-shadow:
			1px 1px 0px 0px,
			2px 2px 0px 0px,
			3px 3px 0px 0px,
			4px 4px 0px 0px,
			5px 5px 0px 0px;

		user-select: none;
		-webkit-user-select: none;
		touch-action: manipulation;
	}

	.button-54:active {
		box-shadow: 0px 0px 0px 0px;
	}

	.button-54:hover {
		box-shadow: 0px 0px 0px 0px;
	}

	@media (min-width: 768px) {
		.button-54 {
		}
	}

	@keyframes gradient {
		0% {
			background-position: 0% 50%;
		}
		50% {
			background-position: 100% 50%;
		}
		100% {
			background-position: 0% 50%;
		}
	}

	.blob {
		position: absolute;
		opacity: 0.8;
		width: 500px;
		aspect-ratio: 1/1;
		/* animation: animate 5s cubic-bezier(0.68, -0.55, 0.27, 1.55) infinite alternate forwards; */
		filter: blur(5px);
		z-index: -1;

		/*  Optional  */
	}

	/* @keyframes animate {
		0% {
			
			border-radius: 60% 40% 30% 70% / 100% 85% 92% 74%;
		}
		50% {
			
			border-radius: 20% 71% 47% 70% / 81% 15% 22% 54%;
			rotate: 41deg;
			scale: 1.15;
		}
		100% {
			
			border-radius: 100% 75% 92% 74% / 60% 80% 30% 70%;
			rotate: -60deg;
			scale: 1.05;
		}
	} */
</style>
