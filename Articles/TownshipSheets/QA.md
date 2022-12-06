"What is this spreadsheet?
- This spreadsheet is NOT a guide on how to play township. It is used for planning out your town using the township template, or to build out your town using some of the builds here. This spreadsheet assumes you have a basic understanding of township mechanics. 
- The builds in here are not min-maxed, so if you want to further optimise it in-game such as further reducing construction resource production buildings, you can do so.
- If you need a guide on township, please check out the links under ""External Guides & Resources""."			
			
			
			
			
"Difference between standalone builds and build series?
- Standalone builds can be followed as long as you have met the requirements and know how to build towards it.
- Build series are a group of builds that are structured to allow you to easily transition from one to the next. They are useful if you have trouble following standalone builds."			
			
			
"How do I edit the Township Template to plan my own town?
To edit, make a copy of this sheet by clicking on 'File > Make a copy' (requires you to be signed in).
"			
			
"How many cemeteries do I need for an XP build?
- If you have positive herbs, potions, clothings, 100% happiness but 0% education, you will need roughly 1 cemetery for every 360 population. 
- Citizens that reach the age of 100 do not add to your dead pile, but simply decay. Thus, when your health is at 100%, you do not require cemeteries as your citizens will decay immediate upon dying."			
			
			
			
"I followed a build which shows 0 dead bodies, but I have plenty of dead bodies from a previous build, what do I do?
When transitioning between builds, you may find that you have a lot of dead overflow from a previous build, which may affect the happiness and health for the build that you are transitioning to. There are 2 options you can choose: 
- If you have a lot of dead bodies (e.g. more than 500K), restarting your town may sometimes be the better option.
- If you have less than 500K, and your town is already very developed, you can convert some of your cheaper or non-essential buildings to cemeteries until your dead reaches 0. The more cemeteries you have (e.g. 300 cemeteries), the faster this process is. This process is also best done when you have high health (see below)."			
			
			
			
			
			
"How is Health calculated? (Courtesy of BinaryDragon)
- Positive increasing Herbs contribute 5%.
- Positive increasing Potions contribute 15%.
- Positive increasing Clothings contribute 15%.
- 100% Education and Happiness each contribute about 42.6%.

This means that you do not require all of the above to hit 100% health necessary to have no dead bodies. "			
			
			
			
			
			
"What is the optimal number of schools and libraries for 100% education? (Courtesy of Gaucho)
Without any education boosts:
    Number of Schools = sqrt[(100 / Education Points from 1 School) * Education]
    Number of Libraries = Number of Schools - 100

With education boosts (e.g. Glacia, Pet, Astrology):
    Number of Libraries = Number of Schools - 100 + (%Boost * 100)"			
			
			
			
			
			
			
"How do I unlock X item in the trader?
When you have obtained an item at least once, they will show up in the trader. To be able to actually trade them, you need to have obtained the item at least 10,000 times. 
"			
			
			
"How is resource production used for upgrading calculated for your builds?
Below are the resource production rates I usually use for the various builds. You can add an extra 50 statues for the additional 15% cost reduction, but I tend to opt for more production buildings. Feel free to build more resource production buildings if you wish to upgrade your buildings faster.

L80 to L99 Builds - Resource production based on how much is needed to upgrade to 1 large cottage every tick at 0% cost reduction:
12150 Stone / 1280 Bars / 1920 Planks

L100 to L109 Builds - Resource production based on how much is needed to upgrade to 1 manor every 2 ticks at 20% cost reduction:
14400 Stone / 1024 Bars / 1536 Rune & Planks

L110 Builds - Resource production based on how much is needed to upgrade to 1 estate every 3 ticks at 20% cost reduction:
19200 Stone / 1365 Bars / 2048 Rune & Planks

L110+ Builds - End-game builds that reduces resource production for upgrading in favour of min-maxing."			
			
			
			
			
			
			
			
			
			
			
			
"Why does your build not include happiness penalty from insufficient potions?
- Even though the tooltip and wiki suggests that penalty from potions is an additive -40% to your happiness modifier, I have found that to not be the case. Looking at the game's code, there is some calculation involving elderly citizens rather than a flat -40%. If I find an easy way to factor that in, or if the code changes in the future, I may add it in."			
			
			
"Why does your build not include potions consumed by Citizens aged 55 and above?
The calculation for this is given as:
Potions Consumed = (Population over 55 / 1,000) * 30

However, I have decided not to include it in the builds and templates, as it will require the user to key in another entry for ""Population over 55"". Given that there are already quite a number of entries, I have chosen to omit it. However, you may use the formula above to calculate it if you wish to know how many potions will be consumed by a given number of population over 55."			
			
			
			
			
