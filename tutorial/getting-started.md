# Getting Started: Designing a CraftOS standard
If you're reading this, you would probably like to propose a new standard to be accepted by
the [ComputerCraft](http://computercraft.info) community. If you follow this guide to the point and eventually get your
standard accepted, your proposal will rest in this repository *forever*, and might
even [get recommended](ToDo:Point this somewhere) and adopted by many CraftOS developers. Is that not what every
programmer wishes for? Let's get you started!

### Step 1: Your Idea
First off, you should realize that *you* are the key to making your standard a reality. You are the person who will be
in charge of creating and maintaining the proposal, at least to the point where it gets rejected or accepted. For that,
you should have an idea of what do you want to be standardized, how, and why. If you haven't decided on these points
yet, chances are that you aren't ready to propose anything, this step cannot be skipped.

### Step 2: Things to Consider
Before moving on, you should ask yourself the following questions, to evade pointless hours of work :stuck_out_tongue:

> Note that, when unsure, you are always free to join our [Gitter chat](https://Gitter.im/oeed/CraftOS-Standards) where
> you can ask for both help and reviews of your proposal, at *any* point! If you find out that no one is online just
> send your message and check back later. If you’re a bit worried or have any concerns you can send a PM (private
> message) to one of the collaborators, who are listed at the very bottom of the [README](../README.md).

* **Has this standard been suggested earlier?** (Check
  the [PR page](https://github.com/oeed/CraftOS-Standards/pulls?q=is%3Apr), it has a search bar!)
* **Is there a superior (recommended) standard already in place?** (Note that while your idea might be revolutionary,
  chances are that the recommended standard is better. Read its documentation well and decide yourself if you really
  want to suggest your proposal instead)

Still here? Good, we'll make one last attempt at scaring you off your journey. Go through this checklist and ensure that
all your answers are 'yes'. If any one of them isn't, your idea probably isn't as good as you might have thought, and
you might want to redesign part(s) of your proposal.

- [ ] **Does your proposal/format really _need_ to be standardised?** Standards exist to increase cross-platform
  compatibility and keep reinventing the wheel to a minimum. In many cases, however, the proposal can be overly specific
  or so simple that standardising it yields little to no benefits.
- [ ] **If your standard gets accepted, will its users _benefit_ from it?** Does your proposal help solve frequent
  issues related to the category it should be used in? Does it help with compatibility (esp. backward and forward
  compatibility with future standard revisions)? Is it easy to use?
- [ ] **Is your proposed standard _easy to use_?** Does it require third-party code or brand new code to be written in
  order to be used properly, or do you intend to pack necessary utilities with the proposal? Are these utilities
  efficient?

(While we haven't got to the coding in this guide (yet), you can check back here at any time to ensure that all answers
are still yes.)

### Step 3: Documentation
Already sure how should the final result look like? Certain that it will be useful? Ready to get to the _real_ work?
Great! You can start writing the docs for your upcoming standard. Just don't create a Pull Request ("PR") yet, as at
this point your proposal probably doesn't match the [required template](./standard-template.md). We will tell
you when to start publishing your work on GitHub soon enough, so stay tuned!

While writing the documentation, you want to explain the format to people who will be using it in the future. You
obviously have to **follow [the guidelines](./standard-template.md)**, but here are a few things to keep in
mind:

* **Don't write a tutorial**
    * This is an official document describing how your standard looks like and how to use the utilities you will be
      creating for it, but not how to create an example application step by step. You should definitely include code
      examples, but only to the required minimum.
* **Know your audience**
    * You are by no way speaking to children (although our community might twist you into thinking so sometimes). The
      document should be targeted at programmers with at least basic Lua knowledge and some experience in the
      field. Don't waste time explaining what a table is, be clear and to the point.
* **Use English**
    * Remember, language is the means of getting a thought from one brain to another without surgery. Don't *make it* a
      surgery. If you aren't a native speaker, ask for help and grammar checks (asking Google Translator doesn't
      count). Don't try to post docs in German then look for somebody willing to translate them. Also, use formal
      language. Technical jargon is accepted (after all, we are programmers).

### Step 4: Code Examples Done Right
Your documentation isn't complete until it contains example code for integrating your standard in other
projects. Examples shouldn't be too extensive (50 lines at most). If your standard is simple enough, you might want to
stick to the code examples instead of writing an [API](https://en.wikipedia.org/wiki/Application_programming_interface)
later on. If that is the case, all code required to deal with your standard has to be included in the
documentation. Otherwise, write up code examples only for dealing with *the library* you will create in step 5. Keep
them to the point, one per every scenario your standard should be used in. More thorough code should be kept elsewhere
(you will be told where in just a moment!).

One thing to note about example code is that it should be easily readable. Every important line should be commented
(i.e. explain what you're doing!) and the code should be well formatted. Preferably, use camel case for all
variables. If your code outputs something to the screen, add a comment with the exact same text. In Markdown, use proper
highlighting for the source code (i.e. ```` ```lua ... ``` ````).

### Step 5: Utilities
> **Note**: While highly recommended, this step is in fact optional. Simple standards, standards that don't involve code
> and standards for which source code wouldn't be reusable for different platforms (such as different operating systems
> or frameworks) don't have to keep a repository for such small amounts of source code (less than 100 lines indented),
> and should instead only stick with code examples as pointed out in step 4. More complex standards should definitely
> provide libraries and APIs for easy adoption.

Adding a few examples to the Markdown document is one thing, but publishing a library for easy manipulation and (more
importantly) adoption of your brand new standard will certainly increase your user base by a ton. Developers love copy
pasta! Since the CraftOS-Standards repository only contains standard docs, you
should [set up your own repo](https://guides.github.com/introduction/getting-your-project-on-github/) as a place for
real code (also check out the [Hello World tutorial](https://guides.github.com/activities/hello-world/) if you aren't
familiar with how GitHub works yet).

Once you've got the repository up and running, you can start to add commits with both code and documentation. Yes, docs
are especially necessary here, since utilities for your standard are technically a different project, and should be
self-contained. Make sure that all API functions are documented. It helps to use
a [GitHub wiki](https://guides.github.com/features/wikis/) which
uses [Markdown](https://guides.github.com/features/mastering-markdown/), the same markup language as your main standard
documentation file.

This is a fairly complex step, and involves some tedious work, as your new library for your standard should support it
perfectly. However, if your proposal appears interesting to other developers, somebody might be willing to help you out
here. Always discuss your ideas and what you are working on at the moment with the growing community
at [our Gitter chat](https://Gitter.im/oeed/CraftOS-Standards).

#### A Note on Licensing
All standards published here on CraftOS-Standards are [licensed](/LICENSE.md) under
the [GNU Free Documentation License](https://www.gnu.org/licenses/fdl-1.3.en.html). **This includes all code
examples**. For the sake of open source software and simplicity alike, your libraries should also be licensed
under [similar FOSS licenses](https://www.gnu.org/licenses/fdl-1.3.en.html). After all, licensing official utilities for
an open source standard under a closed source license wouldn't make much sense.
