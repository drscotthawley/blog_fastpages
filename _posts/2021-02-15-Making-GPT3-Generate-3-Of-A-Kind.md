---
title: "Scottergories: Making GPT-3 Generate 3 of a Kind"
description: In which we test GPT-3's ability to generate members of a category
layout: post
toc: true
comments: true
categories: [classification, scottergories, gpt-3]
image: images/gpt3-3s.png
date: 2021-02-15 19:33:31
hide: false
search_exclude: false

---

{{ page.content | number_of_words | minus: 26}} words,  {{ page.content | number_of_words  | divided_by: 180 | append: " minute read" }}, {{ page.content | number_of_words  | divided_by: 275 | append: " paperback pages" }}

*I'm a computational physicist who spent most of his life only interested in curve-fitting, i.e. "regression." Recently I've become fascinated in "classification" to the point where I'm in the process of writing a popular-level book on classification and categories.  (For a couple recent works that include some of this, see {% cite hawleywhoserules %} and {% cite hawleykruger %}.)*  

In June of 2020, I applied for OpenAI API "GPT-3" {% cite gpt3 %} access immediately upon its announcement... and just heard back eight months later (shortly after I [tweeted something nice about OpenAI's "CLIP" paper](https://twitter.com/drscotthawley/status/1358991822945681409?s=20)).  My proposal was to explore the GPT-3 language model's capacity for handling categories, something I'll refer to loosely by the shorthand of "categorical reasoning" (but don't take this to mean that I assert GPT-3 actually "reasons" anything).  On the form to request access, I wrote:

> “I’m interested in the modeling and representation of categories using machine learning and how this task compares with human traditions in philosophy and psychology, particularly how concepts are intertwined with language. My sabbatical this fall includes writing a popular-level book about the history of classification with a goal towards relating this to the societal impact of deployed machine learning models. (I gave a [talk at Wheaton on this](https://hedges.belmont.edu/~shawley/classy/Wheaton2019talk) last fall.) This interdisciplinary work began in Oxford two years ago and has been partially supported by a grant from the Templeton and Blankmeyer foundations.
>
> One concrete problem related to this effort is the fairly well-posed question of to what extent sophisticated language models contain sufficient categorical ‘knowledge’ and ‘reasoning’ capacity to play (or officiate) a game such as “Scattergories” — in which unusual, **never-before-seen** categories are introduced during play (e.g., “things you’d find under a bed”). Humans do this well, but my experiments so far with Word2Vec embeddings and with GPT-2 (via the [HuggingFace API](https://transformer.huggingface.co/)) have indicate that both are poorly-suited to this task. I am applying for access to the OpenAI API because I’m curious to see how GPT-3 fares. Categorical reasoning is foundational to intelligence, so such a task is relevant both for understanding human intelligence as well as for advancing the development of general artificial intelligence" [the mission of OpenAI].

For examples of just how poorly GPT-2—the older, smaller model—performs at this task, see the "Discussion" below.  Believe me when I say the results were disappointing.

*"GPT-2 had 1.5 billion parameters. GPT-3 has 175 billion."*

Now, with GPT-3 access, we can begin to see how this newer, bigger model performs.  The essence of using the API is the "Prompt".  So, my job is to craft prompts, and then see how well the model responds.  My first experiment with the API involves getting the model to generate "three of a kind":

***Update*:** *Oh, hey, there's a [new paper on GPT-3 prompt-writing](https://arxiv.org/abs/2102.07350) that came out the same day I wrote this post! Guess I'll read that soon.*



## Three of a Kind

Let's see if GPT-3 can expound in threes.  **I'll write my prompt in bold**, and then <u>underlined text will show the model's completion/output</u>. *(Additional commentary from me will be in italics.)*

**This application generates example members of a category. Examples of fruits are apples, oranges and bananas. Examples of birds are** <u>quails, crows and sparrows</u>.  *(Whoa! Not bad! This is with the "davinci" model, with Response Length = 10 tokens, Temperature = 0.7, Top P = 1, etc..all defaults.)*

*(Ok, I wasn't always getting three examples when I'd re-try, so let's make the "three" explicit:)*

**This application generates three example members of a category. Three examples of fruits are apples, oranges and bananas. Three examples of dogs are** <u>Labrador, Rottweiler and Husky</u>. *(Had to increase response length to 15 and then truncate the extra text which read "The input is")*

*(For the following, just assume that I'm truncating unwanted extra text. Also, to save space, I'll refrain from printing the entire prompt I use, and just list the categories...)*

**fish:** <u>salmon, bass and tuna.</u>

**U.S. Presidents:** <u>George Washington, Franklin Delano Roosevelt and Ronald Reagan</u>  *(Whoah, this one triggered the "This completion may contain sensitive content" warning!)*

**philosophers:** <u>Plato, Descartes and Kant.</u>

**things you'd find in a refrigerator:** <u>milk, orange juice and apple juice.</u> (*Sure. But since it's a random sample, let's go again:*)  <u>milk, cheese and vegetable salsa.</u> *(Not bad!)*

**things you'd find under a bed:** <u>a mouse, a handkerchief and a ball.</u> *(Ok, I guess...why not? Again:)*  <u>socks, shoes and books.</u> *(ok...I can buy that.)*

 **80's power ballads:** <u>"Faith" by George Michael, "I Want to Know What Love Is" by Foreigner and "The Power of Love" by Huey Lewis and the News.</u> *(uh...if you say so. At least these are all in the 80s!)*

**household chores:** <u>cleaning, cooking and sweeping.</u> *(or again:)* <u>washing, cleaning and ironing. Three examples of sports are swimming, running and cycling.</u> *(The model added that second sentence all by itself!  Note all of these are gerunds, i.e. -ing words; it didn't say, for example, something odd/wrong like "clean, mop, broom")*

**things you don't want your mom to know about you:**: <u>a. how drunk you were at the last party b. that you smoke pot c. that you plagiarized on that paper for your English class.</u> *(Whoa, have we reached AGI? ;-) And extra points for the use of "a. b. c.")*

**items you take on a trip:** <u>a car, a suitcase and a book.</u> *(You CAN "take" a car, can't you? hah! Nice linguistic anomaly.)*

**fruits of the Holy Spirit:** <u>faith, hope and love.</u> *(I mean, I want share this on @FaithTechHub, so...right? LOL)*

*OK, I am sufficiently impressed and have now gone to get my official Hasbro(TM) Scattorgories game...The following prompts are from the game*

**things that are sticky:** <u>gum, tape and bubble gum.</u> *([Nooice!](https://www.youtube.com/watch?v=SAfq55aiqPc))*

**things you add water to:** <u>eggs, rice and pasta.</u> *(eggs?  Hmm...go again:)* <u>tea, coffee and milk.</u> *(nice. ...wait, milk?. Again:)*  <u>urns, cups, and buckets.</u> *(whoa!)*

 **terms of measurement:** <u>kilometers, centimeters and grams. Three examples of colors are red, blue and green. Three examples of adjectives are red, blue and green. Three examples of verbs are run, jump</u> *(See? It will keep generating categories if you set Response Length longer. Let me make the Response Length even longer, to 200...)*

**terms of measurement:** <u>3, 4 and 5 meters. Three examples of angles are 20 degrees, 40 degrees and 60 degrees. Three examples of countries are Japan, France and Germany.</u> *(Ok and beyond that it just repeats itself and/or repeats similar sentences, like: "The application generates the following sentences.  This application generates verbs.  The application generates the following sentences. This application generates pronouns." and so on)*

**things found in the ocean:** <u>fish, coral and whales. Three examples of things found in the sky are clouds, stars and planets.</u> *(that second sentence was generated by the model)*

**things that are bright:** <u>the sun, the moon and the stars. Three examples of things that are made of wood are tables, chairs and fences.</u> *(Again, the second sentence was generated.  Just in case it's got a heavenly-body fixation, let's go again:)*  **things that are bright:** <u>the moon, the sun and an electric bulb. Three examples of furniture that a household might have are a sofa, a chair and a table.</u> *(Good job!  "furniture" is a tricky category as described by George Lakoff {% cite Lakoff87 %})*

**leisure activities:** <u>simple relaxation, snowboarding and surfing. Three examples of countries are USA, Canada and Mexico.</u> *(Not bad)*

**reptiles/amphibians:** <u>lizards, frogs and crocodiles.</u> *(Ok, that "slashed" construction of "reptiles/amphibians" was literally what was printed on the card. I had not expected GPT-3 to pull that off, but mixing reptiles (lizards & crocodiles) with amphibians (frogs) is pretty cool.  Let's try just reptiles:)*  **reptiles:** <u>lizards, snakes and turtles. Three examples of mammals are cows, sheep and giraffes. In each example, the category is written in bold letters and</u> *(Ok, now that's just cheeky!)*

**things you do online:** <u>search, chat and email.</u>  *(Note how it generates only things that are...arguably..verbs.  Again:)*  <u>checking email, shopping and playing games.</u> *(My goodness, it's full of gerunds!)*

*(Yea, let's try gerunds, and let's bump the Response Length up to 145...)*

**gerunds:** <u>eating, running and swimming. Three examples of adjectives are large, strong and important. Three examples of verbs are write, jump and try. Three examples of adverbs are quickly, happily and carefully. Three examples of adjectives are big, wide and dangerous. Three examples of prepositions are to, in and on. This application generates a category. All examples are of the same gender, number and case. Three examples of nouns are dog, cat and bird. Three examples of adjectives are tall, small and large. Three examples of prepositions are by, for and under. Three examples of adverbs are quickly, slowly and</u> *(SHOW OFF!)*

**terms of endearment:** <u>honey, sweetheart and dear.</u> *(awww)*

*Ok, I've now gone and grabbed my boxed copy of [The Game of Things](https://www.thegameofthings.com/).  Now, keep in mind, some of these things can be of a "suggestive" nature...*

**things you would like to do with chocolate:** <u>eat it, cook with</u>
<u>it and share it with your friend.</u>  *(Uh...ok, that was not at all suggestive, haha!)*

**things you shouldn't do on your honeymoon:** <u>drink, drive and shop. Three examples of good economic policies are low interest rates, an independent central bank and low taxes. (COMPLETION MAY CONTAIN SENSITIVE CONTENT)</u>
*(All very sensible, though not likely to be what you'll hear if you play in a group of humans.  Note that the "goal" of the humans would be to make each other laugh, whereas GPT-3 is just trying to generate high-probability matches. It's basically playing [Family Feud](https://www.familyfeud.com/).)*

**things that warrant an apology:** <u>spilling a drink on someone, saying something rude to someone, and being late for an appointment.</u> *(Yeah, good job GPT-3!)*

**things that would get you fired:** <u>stealing, sleeping on the job and talking back to your boss.</u> *(Sure!)*

**things you would do if you had super-human powers:** <u>play baseball, run in the Olympics and fly to the moon.</u> *(again:)* <u>catch a falling satellite, fly from New York to Tokyo, and make a million dollars.</u> *(Ok.  Sensible answers, and note that all the verb-usage matches.)*

**things you shouldn't try to hold on to:** <u>a pen, a balloon and a cork.  The idea is that you decide whether the example is an example of the category, or not. You click</u>  *(Ok, wait a sec. Not sure about the pen, balloon and cork??, but it seems like it's scraped some aspect of category-naming-games and included it in here! Let's re-do a bunch)*

**things you shouldn't try to hold on to:**
* <u>a taxi, a dead rat and a Volkswagen.</u>
* <u>a hot potato, a hot date and a hot temper.</u>
* <u>a rock, a bird and a balloon.</u>
* <u>a ball, a cat and a balloon. Three examples of things you should be careful with are an axe, a knife and a gun.</u> *(2nd sentence is part of the output)*
*  <u>a balloon, a basketball and a cactus. In the example, the Generate action is used to randomly generate a member of the category. This</u> *(Ok, kudos on the cactus. Not sure where it's getting its category-gaming info from)*

*(Speaking of [Something To Hold On To](https://www.youtube.com/watch?v=5OAaa7B_GmE), let's give it an obscure music task just to see how it does:)*

**songs by Trevor Rabin:** <u>"Racing in the Street", "Big Generator" and "Can I Play With Madness".</u> *(hahaaaha. The first is a Springsteen tune, the 2nd the [title track off Yes' Big Generator album](https://www.youtube.com/watch?v=8W_VC_BgMjo) when Rabin was in the band and supposedly they all shared writing credits, and I would PAY MONEY to see Trevor Rabin cover Iron Maiden's "[Can I Play With Madness](https://www.youtube.com/watch?v=Kvqr366Op3k)"!)*

*(BTW, if you want to hear an incredible cover of "Something To Hold On To," please give [my good friend Rex Schnelle's version a listen](https://soundcloud.com/rextunes/something-to-hold-on-to-master).  Moving on...)*

**things you shouldn't share:** <u>toothbrushes, clothes and pencils.</u> *(I did this over & over and "toothbrushes" was in every output, no matter how high I made the Temperature)*

**things you shouldn't try to do in the dark:** <u>play tennis, play football and drive a car.</u> *(All my retries on this were similarly boring; GPT-3 rarely surprises one with its off-the-wall hilarity)*

*(Speaking of lack of originality, it's amazing how many cards in The Game of Things start with "Things you shouldn't...")*

**things you wouldn't want to find in your sandwich:** <u>a brick, a piece of glass and a dead rat.</u> *(Spot on)*

*(As a resident of Nashville, I'm curious to see if we can make it write a country song; many country songs are just lists of nostalgia for bygone rural America...)*

**things you remember about growin' up on the farm:** <u>mud, worms, and tractors.</u> *(ok, sure)*

**things Daddy used to tell you**: <u>"Don't do that!", "Be nice.", and "Look out!". Three examples of things you are going to do when you grow up are: "travel to the moon.", "write a book", and "learn how to dance". The full Python code is shown below: def make_things(): fruits = ["apple", "orange", "banana"] people = ["Daddy", "Mommy", "Grandpa"] things = ["Don't do that!", "Be nice.", "Look out!"] things = ["travel to the moon.", "write a book.", "learn how to dance."] return fruits, people, things What is the purpose of this application</u> *(Whooooaaa!  What IS this thing?  Is there a human being on the other end of this?  ;-)  .)*

**things you like about your truck:** <u>leather seats, size, and the sound system.</u> *(Eh. Technically valid answers, sensible, high-probability examples.  Nothing "creative" though, of course. Again, only this time I'll crank the Temperature up to 0.97:)* <u>safety rating, engine, and CD player.</u> *(The "trying to win at Family Feud" analogy is apt. Ok, forget the country song. Moving on.)*

**things you wouldn't want a doctor to say to you:**

* <u>"you don't have anything to worry about", "one more time" and "we'll see how it goes".</u> *(The model knew to use quotation marks!  First example seems wrong.)*
* <u>I have good news and bad news, surgery is now a day care procedure and it's not cancer, it's a tumor.</u> *(Uh.. huh?)*
* <u>, "You're dead", "You're pregnant", "You're infected". Three examples of things you wouldn't want a doctor to say to your wife are</u> *(Nice comma usage, and Whoa! Let's do that last one...)*

**things you wouldn't want a doctor to say to your wife:**
* <u>"I'm sorry" "I love you" and "I'm sorry I love you."</u> *(hahaha!)*
* <u>, "I'm afraid you have cancer", "I'm afraid you have AIDS" and "I'm afraid you have syphilis." Three examples of names of big cities are London, Paris and Los Angeles. Three examples of books to read are "War and Peace", "Mein Kampf" and "The Catcher in the Rye".</u> *(Ok, I think it's got the hang of this 3's-generating now! LOL)*

*Last up: I mentioned this to my friend Heather and she asked me how long I get to 'keep playing with it'.  I said "My free trial tokens expire May 15, 2021, and I've already used 6000 out of 300k tokens. So it's basically like joining the Chuck E. Cheese club."  She said, "Nice! I wonder if you can teach it to win at skee ball 😅" Which means now I have to do...*

**things you'd find at Chuck E. Cheese:** <u>video games, a ball pit and tokens. Three examples of dinosaurs are Tyrannosaurus Rex, Triceratops and Velociraptor.</u> *(NOT BAD! I'm going to go again, and if it mentions skee ball, WE'RE DONE.)*
* <u>tokens, pizza and soda.</u> *(good)*
* <u>Chuck E. Cheese himself, his brother, and a clown.</u>  *(Ohhh-kay that's enough for now! haha)*

## Discussion (Preliminary Thoughts)
"Surely this is not a very 'intelligent' task," you say.  "All it does is generate words that have some suitably high probability of being associated with the word in the prompt."  "Since it was trained on the internet, such lists-of-things-in-a-category probably already exist as web pages somewhere anyway"

Right, one could imagine scraping a ton of web pages for text and then training some kind of non-Transformer-based method, maybe even a Bayesian bag-of-words model (like in a simple spam detector) to rank "related words" and pick the top choices.

That's not exactly what's happened here.  Yes, GPT-3 was trained on tons of web pages, yes it "knows" (has a probabilistic model for) word associations, but also...

It is a "few shot learner" so it essentially *instantly* starts giving me outputs like what I want, without having been pre-trained on the task I want it to do.  The fact that it gets singular vs. plural right, and verbs vs. nouns, and *gerunds* correct in its answers is noteworthy.

So far, this is just my first night of access to the API, and it blows away what I could get GPT-2 to do. One can try out various GPT-2 model sizes using the friendly interfaces at [HuggingFace.com](https://transformer.huggingface.co/). For the smallest GPT-2 model, I got

**dogs:** <u>cats.</u>"  *([Womp womp!](https://media.giphy.com/media/1AHESbqpjV1AFSNJdA/giphy.gif))*

The largest GPT-2 model size, however, with suitably adjusted parameters, <u>could generate 3 dog breeds  or 3 U.S. Presidents correctly</u>.  But any of the more "challenging," "speculative" categories (e.g. "things you might...") give even the largest GPT-2 at HuggingFace a hard time:

**things that would get you fired:** <u>the fire alarm, the bathroom sink and the bathroom mirror.</u> *(?? The other various completions generated by GPT-2 when I re-ran it were similarly irrelevant.)*

One further possible remark to my post here: "You realize you aren't really playing Scattergories(tm), right?" Yes of course.  Scattergories involves rolling the dice and getting a letter and having to name a bunch of things that start with that letter. *Pace.* I was never actually wanting to replicate the Scattergories(tm) game engine itself, rather the name of the game was a placeholder for the idea of "categorical reasoning."  Now...could we get GPT-3 to *actually* *play* Scattergories? ...I'm not sure I even ...care?   I'm not sure how you'd write the prompt for that, but I'm open to trying it.  For now, at just my first night of trying things out, this seems remarkably encouraging.

Which means....based on my experience with AI models: If the initial trial is encouraging, that means there's a TON of failure modes you just haven't discovered yet! ;-)  We can probe for those too, another time -- so far I've only used up 1.6% of my free tokens.   There's a lot more that one can do to use the API, and so far I haven't used any of the advanced prompt-making utilities. **Still, for the first foray into the OpenAI API, this was a GREAT experience!**

**P.S.-** OH GEEZ I JUST NOTICED THAT I TAUGHT GPT-3 TO *NOT* USE THE OXFORD COMMA! May a large millstone be tied around my neck...     **Wait wait!** : All that was needed to get it to start generating Oxford-comma-style examples was to add the comma to my one example: "apples, oranges, and bananas." Wow.

## References
