# Getting Started: Designing a CraftOS standard

If you're reading this, you would probably like to propose a new standard to be accepted by the [ComputerCraft](http://computercraft.info) community. If you follow this guide to the point and eventually get your standard accepted, your proposal will rest in this repository *forever*, and might even [get recommended](ToDo:Point this somewhere) and adopted by many CraftOS developers. Is that not what every programmer wishes for? Let's get you started!

### Step 1: Your Idea
You can't spell "your proposal" without "you". You are the person who will be in charge of creating and maintaining the proposal, at least to the point where it gets rejected or accepted. For that, you should have an idea of what do you want to be standardized, how, and why. If you haven't decided on these points yet, chances are that you aren't ready to propose anything, this step cannot be skipped.

### Step 2: Things to Consider
Before moving on, you should ask yourself the following questions, to evade pointless hours of work.

* **Has this standard been suggested earlier?** (Check the [PR page](https://github.com/oeed/CraftOS-Standards/pulls?q=is%3Apr), it has search!)
* **Is there a superior (recommended) standard already in place?** (Note that while your idea might be revolutionary, chances are that the recommended standard is better. Read its documentation well and decide yourself if you really want to suggest your proposal instead)

Still here? Good, we'll make one last attempt at scaring you off your journey. Go through this checklist and ensure that all your answers are 'yes'. If any one of them isn't, your idea probably isn't as good as you might have thought, and you might want to redesign part(s) of your proposal.

- [ ] **Does your proposal/format really _need_ to be standardised?** Standards exist to increase cross-platform compatibility and keep reinventing the wheel to a minimum. In many cases, however, the proposal can be overly specific or so simple that standardising it yields little to no benefits.
- [ ] **If your standard gets accepted, will its users _benefit_ from it?** Does your proposal help solve frequent issues related to the category it should be used in? Does it help with compatibility (esp. backward and forward compatibility with future standard revisions)? Is it easy to use? 
- [ ] **Is your proposed standard _easy to use_?** Does it require third-party code or brand new code to be written in order to be used properly, or do you intend to pack necessary utilities with the proposal? Are these utilities efficient? 

(While we haven't got to the coding in this guide (yet), you can check back here at any time to ensure that all answers are still yes.) 

### Step 3: Documentation
Already sure how should the final result look like? Certain that it will be useful? Ready to get to the _real_ work? Great! You can start writing the docs for your upcoming standard. Just don't create a Pull Request ("PR") yet, as at this point your proposal probably doesn't match the [required template](./StandardProposalGuidelines.md). We will tell you when to start publishing your work on GitHub soon enough, so stay tuned!

While writing the documentation, you want to explain the format to people who will be using it in the future. You obviously have to **follow [the guidelines](./StandardProposalGuidelines.md)**, but here are a few things to keep in mind:

* **Don't write a tutorial**
	* This is an official document describing how your standard looks like and how to use the utilities you will be creating for it, but not how to create an example application step by step. You should definitely include code examples, but only to the required minimum.
* **Know your audience**
	* You are by no way speaking to children (although our community might twist you into thinking so sometimes). The document should be targeted at programmers with at least basic Lua knowledge and some experience in the field. Don't waste time explaining what a table is, be clear and to the point.
* **Use English**
	* Remember, language is the means of getting a thought from one brain to another without surgery. Don't *make it* a surgery. If you aren't a native speaker, ask for help and grammar checks (asking Google Translator doesn't count). Don't try to post docs in German then look for somebody willing to translate them. Also, use formal language. Technical jargon is accepted (after all, we are programmers).

### Step 4: Almost There
Haha, we lied! You are nowhere near the finish.
