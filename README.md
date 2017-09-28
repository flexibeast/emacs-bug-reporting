# A brief guide to reporting bugs in GNU Emacs

i'm not an Emacs dev myself, but i do follow the bug-gnu-emacs list, and have done so for a while now. Based on my observations, i'd like to suggest some things to keep in mind when you `M-x report-emacs-bug`:

* To begin, narrow down where the problem is, or might be. Does the problem appear when you run Emacs with the `-Q` option? If not, then the cause of the problem is likely to be either in your configuration, or in a package you've installed:

  * Firstly, check whether the problem is in your configuration. If you temporarily move your `.emacs`/`init.el`/whatever out of the path Emacs searches for configuration files, start Emacs, and the problem seems to disappear, then your configuration is likely to be the cause:

    * Try running Emacs with the `--debug-init` option. That might quickly help pinpoint the specific line causing issues.

    * If that doesn't help, you'll need to bisect your configuration file. Remove or comment out half of it, and check if the problem is still present; if it is, the problem is probably in the remaining half, and if you don't, the problem is probably in the removed or commented-out half. Then repeat the process with the relevant halves.

  * If the problem continues to present, even when not loading your personal configuration, then a package you've installed might be the problem. Unless it's a package you've installed from GNU ELPA, you need to report the issue to the maintainer(s) of that package, not via `report-emacs-bug`. Note, too, that issues with Org should be first reported to the Org maintainers, even though Org is part of Emacs. If you've installed the package from GNU ELPA, then that package is considered part of Emacs, and the issue can be reported via `report-emacs-bug`.

Otherwise, if you can reproduce the problem when running Emacs with the `-Q` option, you can report it via `report-emacs-bug`.

* Regardless of where you send the report, it should include the following information:

  * Which version of Emacs you're running, on what operating system. If you're running a version of Emacs built directly from source control, refer to the commit you've built from. Otherwise, report the version number (e.g. "25.1"), and where you installed Emacs from: did you compile it from source, did you get it from your Linux distribution's package manager, did you get it using Homebrew on macOS[1], did you get a prebuilt binary for Windows? Finally, report the version of your OS - sometimes something that works fine in Emacs running on one OS version, doesn't work properly on a different version of that same OS.

  * An overview of you did, what you *expected* to happen, and what *actually* happened.

  * A *minimal example* to reproduce the problem. The more effort you require someone to go to in order to reproduce your bug, the more difficult it makes things for them, the more difficult it is to narrow down the issue, and the less likely the problem will be solved. So this:

  "You need to install Bazinga Linux 2005. Then run this script to fetch data from this Web site. Then install my 5000-line `init.el`. Then load up this 10M file into Emacs. Then do `M-x a-useful-command`. See the problem?"

  is .... not helpful. Especially compared to e.g. this:

  "Run Emacs -Q. Evaluate `(setq a-variable "value")`. Type 'wtf', press space, then do `M-x a-useful-command`. I expected 'wtf' to get capitalised in this context, but instead it always gets replaced with 'doh'."

* Note that your report should be *entirely self-contained* - all the essential information should be within your report, and links to Web sites should only be provided to e.g. provide some background information, demonstrate that other people are facing the same or similar problems, etc.

-----

[1] Or, indeed, are you using the version that comes pre-installed with macOS, which was current around the time the first iPhone was released?
