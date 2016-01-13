# CraftOS Standards

[![Join the chat at https://gitter.im/oeed/CraftOS-Standards](https://badges.gitter.im/oeed/CraftOS-Standards.svg)](https://gitter.im/oeed/CraftOS-Standards?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

*Community standard file formats, communication systems, etc. for ComputerCraft and CraftOS 2.0*

If you're developing a program for ComputerCraft or CraftOS 2.0 it is highly recommended to adopt the systems standardised here. It allows for cross-program compatibility and formats/systems that are well thought out.

----

**Attention!** Any standard proposals that _do not follow_ the rules listed below will have a high chance of being _automatically rejected_!

**Watch this space!** It's probably a good idea to Watch this repository so you are notified when a new standard is proposed.

----

## How to Contribute

If you have a standard you would like to propose follow these steps:

1. **Make sure there isn't an existing standard** – the whole point of this repo is to ensure we don't have two [slightly different standards](https://xkcd.com/927/); there should only be one. You can either check the [PR page](https://github.com/oeed/CraftOS-Standards/pulls?q=is%3Apr) or directly browse the [source tree](https://github.com/oeed/CraftOS-Standards/tree/master/) of this repository. You should also look at the Submission Checklist (further down this page).
2. **Develop your standard** – think about the different use cases and try to create clearly defined standards and rules for your standard. If applicable, it's probably a good idea to create an API or example code for your standard.
3. **Write an RFC** – once you have created your standard create a Markdown document which clearly explains what your standard is, how it works and how to use it. If you're at all unsure of what to do, look at the RFCs of accepted standards. Make sure that the document covers your standard extensively, and contains thorough examples. You want your standard to be the most popular one and to be used by as many people as possible, so this step should take the longest amount of time (not counting #7 Discussion).
4. (Optional) **Create a GitHub repository for in-depth docs and example source code** – Markdown is great, but sometimes you just need to express your thoughts in Lua. This step should be taken if the standard needs thorough documentation (such as a [wiki](https://help.github.com/articles/about-github-wikis/)) and/or example code that is either too long to be included in the Markdown document or split into too many files and follows a specific directory structure. Add the link to your newly created repository to the Markdown document from step 3.
5. **Create a pull request** – create a pull request with your completed Markdown file. If you think it belongs in a folder put it in there/create it, but we can easily move it if you're unsure. Any code examples should be embedded in the Markdown file. Your pull request's description should be a explanation of the format and why it's needed, but not too descriptive, that's what the Markdown file is for. Remember that the pull request isn't permanent, it is there to agree upon the standard, the Markdown file is permanent and should have all the detail. However, any full APIs should be uploaded to Pastebin and a link should be added to the Markdown file. *There should be no code files in the repo, markdown only.*
6. **Post a link on the forums** – not everyone pays attention to GitHub. To allow more people to see your RFC create a topic in general directing them to the pull request. The post should simply give a very brief description of what your standard is (i.e. *an method redirecting a terminal over Rednet*). The post's title should also make it pretty obvious it's an RFC (i.e. *RFC: TRoR (Terminal Redirection over Rednet)*). To keep everything centralised it's best to keep discussion of the RFC on the pull request, *NOT* the forums post.
7. **Discussion** – if anyone has any issues or improvements with your standard discuss them on the pull request and change the RFC's markdown file until people have agreed upon the standard. At this point the pull request will be merged, you standard has been accepted!

If you think a pull request should already have been merged @ mention one of the moderators (see below).

## Submission Checklist

If you think you're reading to create your pull request ask yourself these questions:
- [ ] **Does your proposal/format really need to be standardised?** Standards exist to increase cross-platform compatibility and keep reinventing the wheel to a minimum. In many cases, however, the proposal can be overly specific or so simple that standardising it yields little to no benefits.
- [ ] **If your standard gets accepted, will its users benefit from it?** Does your proposal help solve frequent issues related to the category it should be used in? Does it help with compatibility (esp. backward and forward compatibility with future standard revisions)? Is it easy to use? 
- [ ] **Is your proposed standard easy to use?** Does it require third-party code or brand new code to be written in order to be used properly, or do you pack needed utilities with the proposal? Are these utilities efficient? 

## Moderators

- [oeed](https://github.com/oeed)
- [viluon](https://github.com/viluon)
- [Lyqyd](https://github.com/Lyqyd)
- [dan200](https://github.com/dan200)

