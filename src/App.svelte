<script>
	import StackedChart from './StackedChart.svelte';
	import ImageChart from './ImageChart.svelte';
	import Separator from './Separator.svelte';
</script>

<main>
	<h1 id="title">Are socks <i>really</i><br /> that hard to knit?</h1>
	<ImageChart
		imgurl="img/sock-hero.png"
		title=""
	/>
	<h2 id="subtitle">
		An analysis of over 50,000 sock patterns to debunk common sock knitting
		fears
	</h2>
	<h3 id="author">By Luisa Vasquez</h3>
	<div class="story">
		<p>
			I have been knitting on and off ever since I was a kid. I've made many
			scarves and attempted (and abandoned) several sweaters. I'm an adventurous
			maker but it took me years to work up the courage to try knitting a pair
			of socks.
		</p>
		<p>
			Last year I saw someone on Instagram make a pair of socks and I was
			intrigued. I remembered my friend's grandma knitting socks in the corner
			whenever she would visit when we were kids. She was such a pro that she
			would make them from memory and <strong
				>I'd written socks off as too hard for me to try.</strong
			>
		</p>
		<p>
			When I finally decided to give it a go I was hooked! I was surprised by
			how much I enjoyed knitting my first pair of socks. The project was
			portable enough to bring with me everywhere and each new piece (the cuff,
			the heel, the toe) gave me a new skill to learn which kept me engaged.
			Wearing the finished hand-knit socks was deeply satisfying — they felt so
			professional compared to my wonky childhood scarves.
		</p>
		<p>
			It made me wonder why I put off knitting socks for so long. <strong
				>Were socks were really as hard as I thought?</strong
			> And how did they compare to other common knitting projects?
		</p>
		<Separator />
		<h1>Are Socks Hard to Knit?</h1>
		<h2>What does the data say?</h2>
		<p>
			I turned to Ravelry, a knitting and crochet site, to help answer my
			questions. Ravelry is a pattern database and community site. Pattern
			creators can upload patterns to the site for makers to find, and then
			makers can document their projects on the site as well.
		</p>
		<p>
			There are over 54,000 sock patterns and more than two million completed
			sock projects documented on the site.
		</p>
		<p>
			I was curious whether socks were more or less difficult than other
			knitting patterns often attempted by beginners. After completing a pattern
			on Ravelry, knitters can rate the project's difficulty on a scale of 1 to
			10, with 1 being a "piece of cake" and 10 being "very difficult". I
			compared the difficulty of some of these common patterns to see how they
			compared to socks.
		</p>
		<span class="spacer-medium" />
		<ImageChart
			title="Socks are not harder than other common knitting projects"
			imgurl="img/ProjectsDifficulty.png"
			description="Hats tend to be easier, with the largest number of hat patterns falling in the “Easy” category of difficulty. Interestingly, sock, shawl, and sweater patterns all concentrate at a difficulty of 3 — between “Easy” and “Medium”."
		/>
		<span class="spacer-medium" />
		<p>
			The numbers seem to say that socks aren't harder than other common
			knitting projects. <strong
				>So why do socks get such a bad reputation?</strong
			>
		</p>
		<Separator />
		<h1>Why are knitters afraid to knit socks?</h1>
		<p>
			I turned to <a
				href="https://www.reddit.com/r/knitting/comments/1bwfxh9/sock_knitting_myths/"
				target="_blank">reddit</a
			> and asked some fellow knitters why (if at all) they were afraid of knitting
			socks.
		</p>
		<p>Four key <strong>fears</strong> emerged from the reddit conversation:</p>
		<ol>
			<li>Turning the heel</li>
			<li>Double Pointed Needles (DPNs)</li>
			<li>Thin Yarn</li>
			<li>Knitting two of the same thing</li>
		</ol>
		<p>
			I'm going to use data to bust those myths and show that while socks
			definitely require some patience while learning (like any new skill), they
			are certainly not impossible and can be a great joy.
		</p>
		<Separator type="subsection" />
	</div>

	<div class="story">
		<h6>Fear 1</h6>
		<ImageChart
			title="Turning the Heel"
			imgurl="img/Fear1-HeelTurns.png"
			description="The general “fear” around socks usually seems to relate to the so-called “heel-turn”. The most popular replies to the question of sock fear had to do with how media portrayed socks and how those memories made sock heels seem difficult."
		/>
		<span class="spacer-medium" />
		<p>
			Ravelry uses labels to help pattern authors mark their patterns. These
			labels mark the different sock techniques, such as the type of heel,
			knitting direction, stitch patterns and more.
		</p>
		<p>
			I used different colors when knitting this sock to show the cuff, body,
			heel, and toe. On Ravelry, the author of this sock pattern could use
			labels to describe the different elements of the sock.
		</p>
		<ImageChart
			title=""
			imgurl="img/SockTagsExplainer.png"
			description=""
		/>
		<p>
			To see if heels are the hardest part of a sock, I decided to look at
			pattern labels that describe the socks to analyze which labels might
			contribute most to difficulty.
		</p>

		<h6>Fear 1: Debunked</h6>

		<ImageChart
			title="Heels are not what make a sock difficult"
			imgurl="img/HeelDifficulty.png"
			description="Many knitters fear making their first pair of socks because of the dreaded “heel turn”. But patterns tagged with advanced knitting construction, colorwork, or intricate regional / ethnic patterns are more difficult on average than patterns with other labels, which suggest that sock heels are not what make a sock pattern hard."
			makeWide={true}
		/>
		<Separator type="subsection" />
	</div>

	<div class="story">
		<h6>Fear 2</h6>
		<ImageChart
			title="Double Pointed Needles (DPNs)"
			imgurl="img/Fear2-DPNs.png"
			description="Double pointed needles are a set of 5 needles that are commonly used to knit items with a small circumference such as sleeves, small hats, or socks. And it sounds like avoiding these prickly needles is a big reason knitters avoid socks."
		/>
		<p>
			What these knitters may not have known at first, is that DPNs are only <strong
				>one of many</strong
			> ways to knit socks. Other knitters also piped up in the thread to emphasize
			that DPNs aren't as hard as they look, because you're really only ever knitting
			with 2 needles at a time. Some of these knitters expressed that despite their
			fear, once they tried it, knitting socks wasn't nearly as bad as they thought
			- and many have grown to love it like I did.
		</p>

		<span class="spacer-medium" />
		<h6>Fear 2: Debunked</h6>
		<ImageChart
			title="Four types of needles, including DPNs, are recommended in top 20 patterns"
			imgurl="img/NumNeedles.png"
			description="While it's unsurprising that people assume Double Pointed Needles (DPNs) are the only choice, given that 13 out of the top 20 free patterns recommend them, it's worth noting that knitters have many other needle options available. Magic Loop comes in at a close second for the most recommended needle type in the top 20 free patterns."
			makeWide={true}
		/>
		<ImageChart
			title="DPNs are popular choice in top 20 free patterns, but are not the only option"
			imgurl="img/VerticalNeedleMatrix.png"
			description="Patterns list multiple needles to indicate that knitters can choose their needle type from the suggested options. Take a look at the top 20 free patterns to see which needles are mentioned by pattern authors."
			footnote="“No specific” means the pattern had no mention of the needle type in their instructions. If a pattern mentioned several options, like “Your choice: DPNs, Magic Loop using a 32” cable, 9” Circular.” then I included all of the listed options. For consistency in some cases, I translated “long circular” to mean “Magic Loop”."
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
			changed their mind about the process. I started with Magic Loop and
			thought it was really confusing, so I actually completed my first pair of
			socks with DPNs.
		</p>
	</div>
	<Separator type="subsection" />
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
			makeWide={true}
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
	<Separator type="subsection" />
	<div class="story">
		<h6>Fear 4</h6>
		<ImageChart
			title="Having to knit 2 of the same thing"
			imgurl="img/Fear4-TwoOfSame.png"
			description="Commonly known as “second-second syndrome”, some knitters avoid socks because they dread the idea of having to “finish” a project... only to start the exact same one to finish the pair of socks."
		/>
		<h6>Fear 4: Debunked</h6>
		<ImageChart
			title="Although not as common, knitting socks two-at-a-time is an option"
			imgurl="img/KnittingMethods.png"
			description="While knitting one sock at a time, either cuff down or toe up, is the most popular there are patterns for those who'd prefer to knit socks two at a time. This way, by cast off, you have a complete pair of socks instead of needing to start sock number two. This can help with so-called “Second sock syndrome” where people find themselves annoyed at the idea of making another sock."
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
		<Separator />
		<h1>The wonderful world of Sock Knitting</h1>
		<p>
			Many of the sock knitting fears we examined earlier were based on the
			misconception that there was just one way to do something, and that
			specific method was perceived as scary.
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
			Pattern creators use tags on Ravelry to label their patterns and make them
			easier to find By looking at the number of patterns with each tag year
			over year we can see which sock techniques are most prolific.
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
		<Separator />
		<h6>If you've gotten this far and now want to knit a pair of socks...</h6>
		<h1>A small sock knitting pep talk</h1>
		<p>
			Others may disagree, but I don't think there's a "right" or "wrong" type
			of sock to start with. It'll all depend on where you're coming from in
			your knitting journey and what motivates you.
		</p>
		<p>
			I think the most important aspect for new sock knitters is to <strong
				>pick a pattern that holds your hand.</strong
			> A pattern that pauses to explain the new concepts coming up and tells you
			some tips in case you hit a common hurdle.
		</p>
		<p>
			I had already knit the cuff, heel, and half of the foot of my first sock
			before I realized that
		</p>
		<ol type="a">
			<li>I was knitting the sock inside out 😬</li>
			<li>It did not actually fit onto my foot 💀</li>
		</ol>
		<p>
			So I frogged it (knitter speak for: unraveled it) and started over. Every
			sock I make is better than the last.
		</p>
		<p>
			No matter how good the pattern is, you may need some more help along the
			way. As with any new skill, it'll take a bit to get right.
		</p>
		<p>
			But the effort pays off. The data shows that sock knitters tend to be
			overwhelmingly happy with their projects once completed.
		</p>
		<ImageChart
			title="95% of knitters are very happy or happy with their sock projects"
			imgurl="img/SockHappiness.png"
			description="In addition to providing a database of patterns, Ravelry gives makers the option to document their projects. Knitters can rate how happy they are with their projects and most are very happy with their socks. According to their project notes, many knitters are dissatisfied with their socks due to poor pattern instructions, disliked techniques, or undesired fit."
			footnote="These numbers reflect the knitter's self-reported happiness on 2,186,210 sock knitting projects. These percentages are about the same across all knitting projects."
		/>
		<span class="spacer-medium" />
		<p>
			Here are some tips from me (a pretty new sock knitter) to anyone else
			thinking of giving it a try:
		</p>

		<h6>Tip 1</h6>
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
		<p>Here are a few patterns to check out if you're a beginner:</p>
		<ul>
			<li>
				<strong
					><a
						href="https://www.ravelry.com/patterns/library/rye-sock"
						target="_blank">Rye socks by TinCanKnits</a
					></strong
				>. This free sock pattern comes in various sock weights: Worsted (as the
				thickest yarn), DK, and Fingering. The instructions also have little
				illustrations that explain the basics of a sock structure for beginners.
			</li>
			<li>
				<strong>
					<a
						href="https://www.ravelry.com/patterns/sources/vanilla-sock-methods-by-crazy-sock-lady/patterns"
						target="_blank">Vanilla Sock Methods by Crazy Sock Lady</a
					>
				</strong>. This pattern pack contains detailed instructions for knitting
				socks using 3 different types of needles. The accompanying YouTube
				videos are helpful for seeing the techniques in action. There is also a
				<a
					href="https://www.ravelry.com/patterns/library/dk-weight-vanilla-socks"
					target="_blank">DK weight version</a
				> of this pattern.
			</li>
			<li>
				<strong
					><a
						href="https://store.abramsbooks.com/products/the-sock-project"
						target="_blank">The Sock Project by Summer Lee</a
					></strong
				>. If you like learning from a book, and are willing to purchase
				patterns, you should check out this new book by Summer. She walks you
				through 5 different "basic" socks using all sorts of heels and cuffs
				including a toe-up sock. She then introduces you to stripes, ribbing,
				lace, cables, and colorwork for a total of 25 patterns. All with helpful
				tips and funny commentary throughout.
			</li>
		</ul>
		<Separator type="subsection" />
		<h6>Tip 2</h6>
		<h2>Don't be afraid to look things up as you go</h2>
		<p>
			If you're a visual learner like me, YouTube will be your best friend.
			Whenever I'd stumble on a new concept, I'd look it up with the needle type
			I was using (e.g. "Joining in the round DPNs socks").
		</p>
		<ul>
			<li>
				Denise, aka EarthtonesGirl, has a lot of great videos that cover sock
				techniques part by part in the (aptly named) "No Fear Sock Knitting" <a
					href="https://www.youtube.com/playlist?list=PLCZwTjf0a7DHx4GmgjQ1sjqIWczcSmWoz"
					target="_blank">series of videos</a
				>.
			</li>
			<li>
				If you want to follow along knitting a sock from beginning to end with a
				particular needle type I'd recommend checking out CrazySockLady's <a
					href="https://www.youtube.com/playlist?list=PL1AVMWlYaMynXcAbQSrySxqw3LeERSRCw"
					target="_blank">series of videos.</a
				> I used these to learn new types of needles like 9" circulars.
			</li>
			<li>
				Norman, aka NimbleNeedles, has a ton of sock information as well,
				including this <a
					href="https://youtu.be/2-W_0vMNZig?si=ZAPgDQahNUG3G9h9"
					target="_blank">great video on getting a sock started on DPNs</a
				> by joining in the round.
			</li>
			<li>
				VeryPinkKnits also has a series of slow-motion videos for particular
				techniques such as <a
					href="https://youtu.be/9dYP_GeHLG0?si=AB57k9EECTZxUDWj"
					target="_blank">grafting the toe together.</a
				>
			</li>
		</ul>
		<Separator type="subsection" />
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
		<Separator />
		<h1>Give socks a try</h1>
		<p>
			Personally I'm excited to continue on my sock knitting journey. I have a
			slew of different sock techniques I want to try: colorwork and toe-up
			socks are next on my list.
		</p>
		<p>
			I hope some of this sock-difficulty myth-busting might have motivated you
			to give sock knitting a try! In a world of fast fashion and passing
			trends, socks are here to stay. So why not take some time, slow down, and
			learn a new skill - you'll come out the other side with a super cozy pair
			of socks for yourself or a loved one. And maybe you'll discover a new
			knitting passion.
		</p>
		<p>
			Don't just take my word for it. In the reddit thread where I asked
			knitters about their sock fears, plenty of knitters chimed in to say how
			much they too love sock knitting:
		</p>
		<ImageChart
			title=""
			imgurl="img/FinalQuotes.png"
			description=""
		/>
	</div>
	<div id="methods">
		<div class="story">
			<h2>Methods</h2>

			<p>
				The sock pattern data was pulled from the <a
					href="https://www.ravelry.com/api">Ravelry API</a
				>
				using the R package
				<a href="https://github.com/walkerkq/ravelRy">RavelRy</a> on February 4,
				2024. This data was analyzed in R and used to compare the difficulty of tagged
				patterns, show tag trends over the years, compare yarn thickness to difficulty,
				and visualize which sock methods were most common.
			</p>
			<p>
				For the needles used in top patterns, I downloaded the patterns for the
				top 20 free patterns as of March 3, 2024 and then read the patterns and
				created a dataset based on the needles recommended in the pattern.
			</p>
			<p>
				For comparing the difficulty of socks with other common knitting
				projects I referenced the Ravelry website and filtered to only knitting
				projects by project type and recorded the number of patterns that
				appeared at each difficulty level. This data was gathered on April 7,
				2024.
			</p>
			<p>
				This page was built using Svelte and D3, starting with <a
					href="https://github.com/higsch/svelte-d3-starter">this boilerplate</a
				> by Matthias Stahl. All the static charts were made using RAWGraphs or R
				and then designed in Figma. Illustrations were drawn in Procreate.
			</p>
			<p>
				And finally, while working on this project I knit two pairs of socks as
				gifts, the single sock to be photographed for this project, and started
				my first colorwork sock. Waiting for R code to run is a great time to
				sneak in some knitting.
			</p>
		</div>
	</div>
</main>

<style>
	p {
		margin-bottom: 20px;
	}
</style>
