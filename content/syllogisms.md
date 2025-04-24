---
disableComments: true
toc: false
math: true
---

# Solving Syllogisms is Not Intelligence
April 23, 2025 

<span style="color:gray">
<i>(I think that we overvalue logical reasoning when it comes to measuring "intelligence.")</i>
</span>

What do we mean by *intelligence* in the context of cognitive science and AI? One thing that often comes to mind is logical reasoning: deriving conclusions from a set of axioms and rules, or thinking through syllogisms like *"all cats are mammals, all mammals are warm-blooded, therefore all cats are warm-blooded."* 

Until recently, I thought of structured reasoning tasks as central to human (and by extension machine) intelligence. It seemed almost obvious that a "truly" intelligent system would encode abstract notions of, e.g., [same versus different,](https://arxiv.org/abs/2310.09612) and that such a system would have absolutely no trouble with syllogistic tasks. I don't think this is an unpopular opinion: critics of LLMs assert that logical tasks are [essential to "true" general intelligence](https://garymarcus.substack.com/p/llms-dont-do-formal-reasoning-and). Some go on to claim that this type of reasoning is fundamentally incompatible with probablistic next-token prediction. 


But I'm not sure that abstract logical reasoning is quite as fundamental to human intelligence as it seems. In his 1982 work *Orality and Literacy*, Walter Ong references a [book containing a series of interviews](https://dl1.cuni.cz/pluginfile.php/738180/mod_resource/content/0/Luria%20-%20Cognitive-development-its-cultural-and-social-foundations.pdf) by A.R. Luria, a Soviet neuropsychologist who interviewed low-educated populations of peasants in the Uzbek SSR in 1931. The interviews were published over forty years later, in 1976, and are very interesting to me.

Here is one of the questions Luria asked people:

> **In the Far North, where there is snow, all bears are white. Novaya Zemlya is in the far north and there is always snow there. What color are the bears?**

Strikingly, Luria found that illiterate respondents were very unlikely to simply respond "white" to this question. They ignored the constraints of the syllogism, and reasoned based on their own personal experiences instead. Here is an example of an exchange with a 37-year-old from a remote Kashgar village [(Luria, 1976, pp. 109)](https://dl1.cuni.cz/pluginfile.php/738180/mod_resource/content/0/Luria%20-%20Cognitive-development-its-cultural-and-social-foundations.pdf), who refused to accept the premise of the question.

> **In the Far North, where there is snow, all bears are white. Novaya Zemlya is in the far north and there is always snow there. What color are the bears?**<br>
> "There are different sorts of bears." <br>
> **(The syllogism is repeated.)** <br>
> "I don't know. I've seen a black bear. I've never seen any others... each locality has its own animals: if it's white, they will be white; if it's yellow, they will be yellow." <br>
> **But what kind of bears are there in Novaya Zemlya?***<br>
> "We always speak only of what we see, we don't talk about what we haven't seen."<br>
> **But what do my words imply? (The syllogism is repeated.)**<br>
> "Well, it's like this: our tsar isn't like yours, and yours isn't like ours. Your words can be answered only by someone who was there, and if a person wasn't there he can't say anything on the basis of your words." <br>


Luria presents illiterate Uzbeks with many more logical puzzles, which they also seem to reject. When shown drawings of an axe, a saw, a hatchet, and a log, and asked to choose the odd one out, a 25-year-old illiterate respondent said: "They're all alike. The saw will saw the log and the hatchet will chop it into small pieces. If one of these has to go, I'd throw out the hatchet. It doesn't do as good a job as a saw." Literate respondents, on the other hand, would almost always discard the log, with the rationale that the three tools should be grouped together. 

Regardless of the underlying explanation for this behavior, I find these interview responses thrilling to read. There are a lot of hypotheses for why these people were so resistant to such logic-based tasks (e.g., Ong points out that peasants who had learned to write were more likely to entertain Luria's syllogisms), but there is no reason to believe that regular people born in the Uzbek SSR and randomly selected for this study were any more or less "intelligent" than individuals drawn from some other population. Clearly, abstract reasoning tasks like deduction and categorization are *not* universal across humans—and these Uzbek farmers were getting along just fine without much care for them!

### Some Sympathy 

To go back to the bear example, it's not that people *couldn't conceive* of the abstract reasoning necessary to answer this problem "correctly." After more back-and-forth in the above conversation, another young Uzbek chimed in, who was clearly able to complete the syllogistic reasoning presented in the question.

> **But on the basis of my words—in the North, where there is always snow, the bears are white, can you gather what kind of bears there are in Novaya Zemlya?**<br>
>"If a man was sixty or eighty and had seen a white bear and had told about it, he could be believed, but I've never seen one and hence I can't say. That's my last word. Those who saw can tell, and those who didn't see can't say anything!" (At this point a young Uzbek volunteered, "From your words it means that bears there are white.")<br>
>**Well, which of you is right?**<br>
>"What the cock knows how to do, he does. What I know, I say, and nothing beyond that!"

Reading the transcripts of these interviews, it seems to me that these questions are just frustratingly uninteresting to the interviewed subjects, who were not used to contrived tests of formal reasoning in classroom settings. It's not unreasonable to respond this way if you aren't used to separating a word problem from the world that it is embedded in (sequestering it away in a little [closure](https://en.wikipedia.org/wiki/Closure_(computer_programming))). 

Here's an example that might make you more sympathetic to the Uzbek nomads. What valid inference can you make based on the following statements ([Byrne, 1989](https://modeltheory.org/papers/1989suppression.pdf))?

<!-- http://repo.darmajaya.ac.id/4379/1/Computational%20logic%20and%20human%20thinking%20_%20how%20to%20be%20artificially%20intelligent%20%28%20PDFDrive%20%29.pdf
https://modeltheory.org/papers/1989suppression.pdf -->

> If Amy has an essay to write, she will study late in the library.
<br> If the library is open, Amy will study late in the library. <br> Amy has an essay to write.

Here you are supposed to reason logically within the confines of these three sentences, which translated into symbols, say: $P\rightarrow Q$, $M\rightarrow Q$, $P$. Operating logically, I know that I can conclude $Q$. But personally, I find it very hard to conclude that "Amy will study late in the library" without knowing whether the library is open. There is an obvious *modus ponens* here, but I just cannot make myself believe it. Others agree: 62% of respondents in Byrne's original study made the same "error" that I did. 

So—if you agree with me that we can't conclude whether Amy will study late unless we know the closing hours of the library she plans to study at, then maybe you can understand the indignation of the 37-year-old Uzbek when asked whether bears in Novaya Zemlya are white. When situated in a real life scenario, it just doesn't make sense to reason in this way. Suspending all external world knowledge and understanding to complete a word problem just feels inane. We are used to suspending our disbelief when it comes to classic syllogisms, but once the reasoning hits a little closer to home, a lot of us end up reacting just like Luria's interviewees. 

## Quick Conclusion 

So, is the skill of suspending disbelief in order to activate particular logical processes, given a particular type of question, a good indicator of general intelligence? Maybe our focus on "intelligence" is myopic in and of itself. In *Orality and Literacy*, Ong notes that people from oral cultures do not think of individuals as being "intelligent" in general. If someone is a good navigator, they are a good navigator. If they are a dancer or storyteller, they are lauded for those abilities. Why would you need some underlying g-factor to tie all of these traits together? (And in the case of IQ testing, why would shape rotation and syllogism questions be uniquely suited to measure that factor?)

Ironically, I'm now suspicious of the word "intelligence" in AI research when it refers to these narrow abstract reasoning tasks. Not just because of pedantic nitpicking, not just because of the horrible history of IQ testing ([in which the Binet-Simon IQ test was leveraged by eugenecists to sterlize 60,000 people in the U.S.](https://en.wikipedia.org/wiki/Intelligence_quotient#IQ_testing_and_the_eugenics_movement_in_the_United_States)), but because I simply think it's a really narrow view of the human mind, which makes it unhelpful for our purposes as AI researchers. 

<!-- 
The word problems in this anecdote are clearly reminiscent of how we measure IQ in intelligence testing. One conclusion that you might draw from this is that if illiterate people are less good at  -->
