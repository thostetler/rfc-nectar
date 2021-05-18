# Comments on the RFC

I will add my comments here into one section; it is because the RFC is evolving - and when I collected the information, it was reflective of the previous version of RFC. But also I'm hoping to present a coherent block of thoughts, so it will hopefully be not too distractful to have it in one section. So please adjust your interpretation to what is your current understanding of the existing RFC

## Main observation:

I would recommend that you carefully review requirements and the direction of the new system - I have arrived at a conclusion, further confirmed by discussions, that the overarching design goal was to serve the bots/non-js agents. This "one goal" naturally led to other outcomes, but it would be my recommendation that you reconsider the goal/architecture from the perspective of building new UI from a broader perspective, with loftier goals in mind - i.e. to be better in all current aspects, not just one. It doesn't need to be qualitatively better - (evolution rather than revolution) - but the aspirations could/should be higher, more far reaching.

> I wouldn't say that we necessarily considered the non-js users/bots our "one goal." Just that we wanted to build the new app with this as a core design feature. I agree that we should think bigger, however the original idea for this was to replace the underlying technology while keeping the current feature set. This project main goal being a fix for several pain points that exist in the current Bumblebee application, from both implementation and development.

The current RFC (as I see it today) is an improved version of the previous RFC; but I'm still missing a comprehensive vision. The effort to formulate in your minds a vision of what you want to build could be enhanced. The exploration/prototype is informing it, but you may want to be careful which path you'll take: 1) have a vision that gets updated/modified based on what you encounter, or 2) have your vision formed by the (accidental) encounters with the reality.

I obviously, personally, prefer the first approach. So I'd recommend that you really try to develop a mental model of what you are designing first and verify it against the reality later.

Maybe that mental model is already present (and I'll speak later to what I have encountered while listening and exploring the prototype) - but if it is the case already, then I'd at least recommend that you spent little bit more energy of communicating that vision - making it coherent and strong, so that it can withstand scrutiny of prying eyes. We want to do X, because doing Y,Z,W would have those other problems….

I'd also note that the RFC has been mostly written by Sergi, that was surprising to me as well given what I learnt later, that his interpretation of the existing prototype state was no aligned with Tims's. Whoever takes charge (and assumes responsibility) for the new system is the one who also develops the vision and puts it in writing, presently it might not be as clear who took responsibility for the decision (who is in charge).

## Going from 20.000 feet to 10.000:

The few paragraphs above are my main comment, it concerns strategy (and strategic vision). If we go lower, then I'd like to make you think little bit harder about the following question:

- if we enlarge (or change) the scope/goals of the project, should we re-visit the chosen technologies/patterns?

For example, it seemed to me that you have concentrated on a particular feature (non-js users/bots) but the other features did not seem to receive the same amount of consideration. If you were to approach it differently, would you have picked the same technology?

As an example, think about the following:

The current system is engineered around the ability to generate pages so that they are easy to generate static pages. We have joked about it (JS world has discovered PHP), but jokes aside, this decision simply stems from the overarching desire to make the statically generated pages possible (to remove ADSCore), and the remaining concerns become secondary. But you could approach the new system with a slightly different perspective too:

- How can we build a system that is modern, takes advantage of all developments that JS community created _AND ALSO_ can support statically generated pages?

Would your answer be the same? Maybe. But I would like to urge you to seriously consider it. For it seems to me that you put too much emphasis on certain features, but those features aren't the only features/variables of the equation.

From my perspective (which is generic and may be misguided, but worth thinking about at least) I'd be asking the following question:

- Can we find a framework for building web applications which can support the requirement for statically generated pages?

And I mean _framework_, not a library. A mature framework with a community, established patterns, and ways of doing things. That is one thing that BBB got wrong: we picked a 'wrong' library. If we had picked a framework, we could have maybe not had to rewrite BBB in a new technology (on the other hand, even established frameworks cannot guarantee that - as the pain around Angular v1 vs v2 proves).

> I think that the choice to go with Next.js wasn't just about improving SEO. One of the biggest complaints about Bumblebee was speed. With this hybrid approach we can get some real speed improvements. Not to mention that Next.js makes this whole process much easier by dynamically choosing how to render a page, and prefetching.
> We can also take advantage of incremental static generation, or statically generating a set of top abstract pages for example, further reducing server cycles.

> Next.js is really it for production-ready frameworks, we could do some of this ourselves using vanilla React however. That is always an option, however I think the benefits of using a framework like Next.js really outweigh the downsides.

## Going down to 5.000 feet

With a framework, one is constrained by how things get done - but that might be a curse and blessing too. One real advantage is to have the patterns and components that have been already developed/contributed. That is a serious decision: do you have enough good reasons to want to build many parts of the system yourselves? Again, the answer always is: "it depends on what you want to accomplish" -- but as I tried to tell you in the first paragraph, I think what you set yourselves as goals initially was not bold enough, and broad enough to build. IMHO you should aim higher.

## The rest

The rest of my comments are just inconsequential musings:

- TypeScript is not a problem, strongly typed languages are great if they help you develop and maintain large projects. Mind however the complexity of the build tools and all the extra overhead. It seemed far from being easy or helpful or simple. It rather seemed there were more layers of abstraction, with longer debugging cycles. So it would be beneficial to look at it carefully, whether the benefits are bigger than costs
- monorepo: a particular solution for a dependency hell, but it also seems it makes any application grow bigger. That might backfire if one has to optimize or simply desires to have a simple codebase (there are no free lunches - we can't go lean without some pain in actually carefully incorporating code; in frameworks, that pain is sometimes offloaded to core developers...)
- speed: examine carefully and actually try to estimate the necessary resources for rendering the web pages. You now know very precisely how many pages ADS is generating now (we didn't have such luxury before), if you also estimate how long it takes to generate one on average, then you can arrive at the expected required hardware to serve ADS users. This step should be done early. Think what happens if the system has to grow x-fold.

This concludes my notes.
