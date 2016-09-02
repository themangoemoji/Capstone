# Meeting With Mozilla


#### Mike & Jared's Expertise
* Mike:
  * Working on e10s team.
  * A generalist 

* Jared:
  * Focused on visual changes and things that are buttons, menus, user interaction pieces
  * Video controls, plugins, scrolling
  * Frontend general styling and pop-up expertise
  * His 4th Capstone


#### Project Overview:
* [The Bug Report](https://bugzilla.mozilla.org/show_bug.cgi?id=1091592)
* [The Spec](https://bug1091592.bmoattachments.org/attachment.cgi?id=8776005)

* **NOTE:** The two major tasks are in parallel

* **Task One** - Merge single and multiprocess dropdown
  * **e10s** = Electrolysis: the splitting of firefox into multiple processes so that the browser remains responsive when processes are running
    * Basically, Mozilla is in the process of slicing the browser and trying to let these processes talk between the gap
    * When you click on select dropdown, the child process that is run is different between multiprocess and single-process. You cant open a window from a content process. 
    * Content(?) process and chrome process (nothing to do with google chrome) are now separate, we need to unite them.

* **Task Two** - Styling of dropdown and added functionality
  * Checking for accessibility and whether the inputs make sense
    * Firefox has very high standards for accessibility.

* One or two people can work on styling, another group can work on porting
* **(`AI`)** Decide how we want to manage/divide the team.
* We're also going to need to make sure whatever we ship that we can turn it off for anyone (like a feature flag)
  * Many of these types of things are found in `about:config` (you can type that in the URL bar) 
  * These are all internal flags, booleans, half baked stuff, memory alloc, etc.


#### Communication
> You've been trained to work alone, if we are confused or blocked --> Ask the questions!
> You have opportunity to talk to anyone at mozilla, we can ask the code authors about their implementations, we don't want to limit you

Tips:
* Pinging/Typing name to get ahold of people on IRC
* Ask questions in `fx` channel, if Mike & Jared don't answer, someone else will!
* Option for free IRC --> We could spin up our own server and install IRC bouncer
* **(`AI`)** Expense Cloud IRC accounts
* **(`AI`)** - look into the possibility of traveling to Toronto early and front-loading this project


#### Development Tips
* People are afraid of looking stupid (print statements, garbage, etc.), but don't be scared, get feedback early for course correction.
* Project plan: "we have a project plan... but" --> they want to see us develop and figure it out & learn. Theres a lot we won't know.
* Artifact Builds --> They are awesome, they should take 2 mins to do a full build. The C++ builds (compiled languages) are exempt from these.
* How do Artifact Builds work?
  * When something gets built, we run through tests and build servers, we keep the build output as an executable. When you do an artifact build, we use these cached build files by first downloading them, placing and copying these build files into your directory,
  * This is only for JS, HTML, CSS, because these are not compiled. If you are making incremental changes, they should take 2-3 seconds. Even full builds should be < 1 min.
  * [We can grab these Artifact Builds from moz/config ](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Build_Instructions/Artifact_builds). It is required to set the flag 'enable artifact builds'


#### The C++ task specifics
> The C++ code is ... whoa. We'll only be looking at a small part of it. Don't freak out.
* [The forking statement for the two procecess](http://searchfox.org/mozilla-central/source/layout/forms/nsListControlFrame.cpp#1852)
* What Mike explained about the code:
  * The single process method shows its own pop-up, the multiprocess way uses another. [The fork for the popup choice happens here](http://searchfox.org/mozilla-central/source/layout/forms/nsListControlFrame.cpp#1852)
  * `nsListControlFrame` is what you see in a select thing that you click. 
  * When you click, via a `MouseDown` event, stuff goes on through lines 1769...1840. Eventually we get a `mComboboxFrame`. This draws the item we click on (the frame). 
  * There is a `listcontrolframe` (the whole dropdown menu) and it has a `comboboxfrome` (the right half of it the dropdown... at least Mike thinks so). 
  * **NOTE:** A frame anything that is drawn. 
  * When we fire `FireShowDropDownEvent`, we check to see if we're in `contentprocess`, if we are, we dispatch an event that JS is listening to, and return true.
  * Also, there was something important about `MComboBox` frame... look into it


#### Next Steps
* **(`AI`)** [Get oriented with codebase](http://searchfox.org/mozilla-central/source), specifically [the browser `.xul` markup file](http://searchfox.org/mozilla-central/source/browser/base/content/browser.xul)
* **(`AI`)** Things to research: Firebug, webkit inspector, firefox developer tools and browser toolbox
* **(`AI`)** [Become familiarized with `hg` (Mercurial)](http://mozilla-version-control-tools.readthedocs.io/en/latest/hgmozilla/)
* **(`AI`)** [The Browser Toolbox](https://developer.mozilla.org/en-US/docs/Tools/Browser_Toolbox), learn how to use it.
* **(`AI`)** Manipulate part of the browser, styles to mess around with developing browser
* **(`AI`)** Learning how to use debugger
* **(`AI`)** Make pertinent accounts (bugzilla, etc.)
* **(`AI`)** Schedule these meetings weekly
