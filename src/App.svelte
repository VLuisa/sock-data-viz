<script>
	import StackedChart from './StackedChart.svelte';
	import Matrix from './Matrix.svelte';
	import ImageChart from './ImageChart.svelte';
	import Separator from './Separator.svelte';
</script>

<img
	src="img/Header-Desktop.png"
	alt="Are socks really that hard to knit?"
	style="width: 100%"
/>
<main>
	<div class="story">
		<h1>Are Socks Hard to Knit?</h1>
		<p>
			I have been knitting ever since I was a kid. I've made many many scarves
			and attempted (and abandoned) several sweaters. I found scarves to be
			great gifts but quite boring to knit. Sweaters took far too long and I
			lost interest quickly.
		</p>
		<p>
			Last year I saw someone on Instagram make a pair of socks and I was
			intrigued. I remembered my friends Grandma knitting socks in the corner
			whenever she would visit, <strong
				>but I'd always thought socks were too hard to try.</strong
			>
			But when I finally gave it a try, I was hooked!
		</p>
		<p>
			Having a hand-knit pair of socks was deeply satisfying. The project was
			portable enough to bring with me everywhere and each new piece (the cuff,
			the heel, the toe) gave me a new skill to learn which kept me engaged.
		</p>
		<p>
			It made me wonder why I put off knitting socks for so long. Were socks
			really as hard as I thought? How did they compare to other common knitting
			projects?
		</p>
		<h2>Investigating sock difficulty through data</h2>
		<p>
			I decided to use Ravelry, a knitting and crochet site, to help answer my
			questions. There are over 54 thousand sock patterns and more than 2
			million completed sock projects documented on the site.
		</p>
		<span class="spacer-medium" />
		<ImageChart
			title="Socks are not harder than other common knitting projects"
			imgurl="img/ProjectsDifficulty.png"
			description="Sock, shawl, and sweater patterns concentrate at a difficulty of 3 — between “Easy” and “Medium”. Hats tend to be easier than these other projects, with the largest number of hat patterns falling in the “Easy” category of difficulty. All project types have patterns across the full range of difficulty."
		/>
		<p>
			The numbers seem to say that socks aren't harder than other common
			knitting projects. <strong
				>So why do socks get such a bad reputation?</strong
			>
		</p>
		<Separator />
		<h1>Why are knitters afraid to knit socks?</h1>
		<p>
			I turned to reddit and asked some fellow knitters why (if at all) they
			were afraid of knitting socks.
		</p>
	</div>

	<div class="story">
		<h6>Fear 1</h6>
		<ImageChart
			title="Turning the Heel"
			imgurl="img/Fear1-HeelTurns.png"
			description="The general “fear” around socks usually seems to relate to the so-called “heel-turn”. The most popular replies to the question of sock fear had to do with how hard media made sock heels seem."
		/>
		<span class="spacer-medium" />
		<h6>Fear 1: Debunked</h6>

		<span class="spacer-medium" />
	</div>
	<ImageChart
		title="Heels are not what make a sock difficult"
		imgurl="img/HeelDifficulty.png"
		description="Many knitters fear making their first pair of socks because of the dreaded “heel turn”. But patterns tagged with advanced knitting construction, colorwork, or intricate regional / ethnic patterns are more difficult on average than patterns with other tags, which suggest that sock heels are not what make a sock pattern hard."
		makeWide={true}
	/>
	<Separator />
	<div class="story">
		<h6>Fear 2</h6>
		<ImageChart
			title="Double Pointed Needles (DPNs)"
			imgurl="img/Fear2-DPNs.png"
			description="Double pointed needles are a set of 5 needles that are commonly used to knit items with a small circumference such as sleeves, small hats, or socks. And it sounds like avoiding these prickly needles is a big reason knitters avoid socks."
		/>
		<p>
			What these knitters may not know though, is that DPNs are only <strong
				>one of many</strong
			> ways to knit socks. Other knitters also piped up in the thread to emphasize
			that DPNs aren't as hard as they look, because you're really only ever knitting
			with 2 needles at a time.
		</p>

		<span class="spacer-medium" />
		<h6>Fear 2: Debunked</h6>
		<ImageChart
			title="DPNs dominate top 20 free patterns, but are not the only choice"
			imgurl="img/VerticalNeedleMatrix.png"
			description="While it's unsurprising that people assume Double Pointed Needles (DPNs) are the only choice, given that 13 out of the top 20 free patterns recommend them, it's worth noting that knitters have many other needle options available. In fact, just across the top 20 patterns, 4 different types of needles are recommended."
			footnote="“None specified” means the pattern had no mention of the needle type in their instructions. If a pattern mentioned several options, like “Your choice: DPNs, Magic Loop using a 32” cable, 9” Circular.” then I included all of the listed options. For consistency in some cases, I translated “long circular” to mean “Magic Loop”."
		/>
		<span class="spacer-medium" />
		<p>
			In my sock knitting journey I've tried DPNs, Magic Loop, and 9" circulars.
			They all provide unique knitting experiences and have their pros and cons.
			I'm still learning and exploring and eventually I, like most sock
			knitters, will have my favorites.
		</p>
		<p>
			Some people who started with a certain method and were discouraged found
			that returing to sock knitting with a different approach completely
			changed their mind about the process.
		</p>
	</div>
	<Separator />
	<div class="story">
		<h6>Fear 3</h6>
		<ImageChart
			title="Thin Yarn and Tiny Needles"
			imgurl="img/Fear3-ThinYarn.png"
			description="Many knitters who are used to making sweaters or scarves, tend to use medium weight yarns and are intimated by the prospect of the thinner yarn they see as required for socks."
		/>
		<h6>Fear 3: Debunked</h6>
		<ImageChart
			title="Not all sock patterns require Fingering weight yarn"
			imgurl="img/YarnWeightAndDifficulty.png"
			description="Although Fingering weight yarn is the most popular choice for socks, there are sock patterns with thicker yarn weights that tend to be easier."
			footnote="Only includes patterns with one or more difficulty ratings and a description of the yarn weight: 20,568 patterns out of total 54,223 sock patterns"
		/>
		<span class="spacer-medium" />
		<p>
			If knitters want to try socks without going down to too thin of a yarn, DK
			is a popular choice. It can introduce you to the new core concepts of
			socks and work up much more quickly than Fingering.
		</p>
	</div>
	<Separator />
	<div class="story">
		<h6>Fear 4</h6>
		<ImageChart
			title="Having to knit 2 of the same thing"
			imgurl="img/Fear4-TwoOfSame.png"
			description="Commonly known as “second-second syndrome”, some knitters avoid socks because they dread the idea of having to “finish” a project... only to start the exact same one to finish the pair of socks."
		/>
		<h6>Fear 4: Debunked</h6>
		<ImageChart
			title="Although not as common, knitting socks two-at-a-time can help with second sock syndrome"
			imgurl="img/KnittingMethods.png"
			description="While knitting one sock at a time, either cuff down or toe up, is the most popular there are patterns for those who'd prefer to knit socks two at a time. This way, by cast off, you have a complete pair of socks instead of needing to start sock number two."
			footnote="Two-at-a-time is illustrated here as two socks knit from the cuff down with one set of needles but can also be done from the toe up or with two circular needles."
		/>
		<span class="spacer-medium" />
		<p>
			The trade-off with two-at-a-time is that your whole sock project takes
			longer. Personally I like the speed of knitting up one sock by itself, and
			I'm usually excited enough to wear the pair that I don't mind starting in
			on the second sock. Like most things, this really comes down to personal
			preference!
		</p>
	</div>
	<div class="story">
		<h1>The wonderful world of Sock Knitting</h1>
		<p>
			Many of the sock knitting fears we examined earlier were based on the
			misconception that there was just one way to do something, and that that
			particular method was scary.
		</p>
		<p>
			Knowing what is available can make it easier to pick a new path when you
			hit a dead end, and different techniques can really change both the
			knitting experience and the final fit of the socks.
		</p>
		<p>
			It's important to know that, just as there are many different types of
			needles, and sock directions, there are many different ways to approach
			each part of a sock.
		</p>
		<p>
			Pattern creators use #tags on Ravelry to help make it easier to find their
			patterns. By looking at the number of patterns with each tag year over
			year we can see which sock techniques are most prolific.
		</p>
		<StackedChart />
		<div class="spacer-medium" />
		<p>
			If you're considering making your first pair of socks, beginning with
			well-known sock methods like a heel flap and gusset can be a great choice.
			Mastering this technique opens the door to thousands of other patterns for
			you to explore.
		</p>
	</div>
	<div class="story">
		<h6>If you've gotten this far and now want to knit a pair of socks...</h6>
		<h1>A small sock knitting pep talk</h1>
		<p>
			Others may disagree, but I don't think there's a "right" or "wrong" type
			of sock to start with. It'll all depend on where you're coming from in
			your knitting journey and what motivates you.
		</p>
		<p>
			I think the most important aspect for new sock knitters is to pick a
			pattern that holds your hand. That pauses to explain the new concepts
			coming up and tells you some tips in case you hit a common hurdle.
		</p>
		<p>
			However, no matter how good the pattern is, you may need some more help
			along the way. As with any new skill, it'll take a bit to get right.
		</p>
		<p>
			I had already knit the cuff, heel, and half of the foot of my first sock
			before I realized that a) I was knitting the sock inside out and b) it did
			not actually fit onto my foot.
		</p>
		<p>
			So I frogged it (knitter speak for: unraveled it) and started over. Every
			sock I make is better than the last.
		</p>
		<h6>Tip 1</h6>
		<h2>Don't be afraid to look things up as you go</h2>
		<p>
			If you're a visual learner like me, YouTube will be your best friend.
			Whenever I'd stumble on a new concept, I'd look it up with the needle type
			I was using (e.g. "Picking up stitches DPNs socks").
		</p>
		<h6>Tip 2</h6>
		<h2>Know what motivates you</h2>
		<p>
			Although I knew that DK socks would work up faster, I really wanted socks
			that felt like socks not slippers and that suited my slightly warmer
			climate so I stuck with Fingering. This definitely took longer but left me
			more satisfied with what I wanted.
		</p>
		<p>
			Others may prefer to start with DK as a "practice" sock and move on to
			Fingering and that's ok too!
		</p>
		<h6>Tip 3</h6>
		<h2>Recognize your skills</h2>
		<p>
			If you're already a knitter, odds are you know way more than I did when I
			started my first pair of socks.
		</p>
		<p>
			Which is to say, lean into your strengths. If you already know cabling or
			colorwork and are motivated by that intricacy while you work, then find a
			sock pattern that will incorporate those elements in.
		</p>
		<p>
			This is a great <a
				href="https://www.ravelry.com/patterns/library/maine-coast-summer-socks"
				target="_blank">cabled sock</a
			>
			by Summer Lee Knits and I love all the
			<a
				href="https://www.ravelry.com/designers/stone-knits"
				target="_blank">fun colorwork patterns</a
			> by Stone Knits.
		</p>
		<h1>Final words</h1>
		<p>Some recommended patterns...</p>
	</div>
</main>

<style>
	/* Add any custom styles here */
	main {
		display: flex;
		flex-flow: column nowrap;
		align-items: center;
	}
	p {
		width: 50vw;
		/* max-width: 600px; */
		margin-bottom: 20px;
	}
</style>
