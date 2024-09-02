# Programming with Python

This lesson is based on [Library Carpentry][lc-site]'s [Python Intro for Libraries][lc-python].

An introduction to Python for non-programmers using inflammation data.

## About the Lesson

This lesson teaches novice programmers to write modular code to perform data analysis
using Python. The emphasis, however, is on teaching language-agnostic principles of
programming such as automation with loops and encapsulation with functions,
see [Best Practices for Scientific Computing][best-practices] and
[Good enough practices in scientific computing][good-practices] to learn more.

The example used in this lesson analyses a set of 12 files with simulated inflammation
data collected from a trial for a new treatment for arthritis. Learners are shown
how it is better to automate analysis using functions instead of repeating analysis
steps manually.

The rendered version of the lesson is available at:
[Programming with Python](https://broadinstitute.github.io/2024-06-24-python-novice-lesson/).

The Carpentries also offers versions of this lesson in [R] and [MATLAB].

## Episodes

| \#   | Episode | Question(s)                                                                  |
| --: | :------ | :--------------------------------------------------------------------------- |
| 1   | [Python Fundamentals][episode01]        | What basic data types can I work with in Python?<br>How can I create a new variable in Python?<br>Can I change the value associated with a variable after I create it?                             |
| 2   | [Analyzing Patient Data][episode02]        | How can I process tabular data files in Python?                              |
| 3   | [Visualizing Tabular Data][episode03]        | How can I visualize tabular data in Python?<br>How can I group several plots together?                                  |
| 4   | [Storing Multiple Values in Lists][episode04]        | How can I store many values together?                                        |
| 5   | [Repeating Actions with Loops][episode05]        | How can I do the same operations on many different values?                   |
| 6   | [Analyzing Data from Multiple Files][episode06]        | How can I do the same operations on many different files?                    |
| 7   | [Making Choices][episode07]        | How can my programs do different things based on data values?                |
| 8   | [Creating Functions][episode08]        | How can I define new functions?<br>What's the difference between defining and calling a function?<br>What happens when I call a function?                                              |
| 9   | [Errors and Exceptions][episode09]        | How does Python report errors?<br>How can I handle errors in Python programs?                                               |
| 10  | [Defensive Programming][episode10]        | How can I make my programs more reliable?                                    |
| 11  | [Debugging][episode11]        | How can I debug my program?                                                  |
| 12  | [Command-Line Programs][episode12]        | How can I write Python programs that will work like Unix command-line tools? |

## Contributing

We welcome all contributions to improve the lesson!
Maintainers will do their best to help you if you have any questions, concerns,
or experience any difficulties along the way.

We'd like to ask you to familiarize yourself with our [Contribution Guide](CONTRIBUTING.md).

## Maintainers

Lesson maintainers are Jean Chang and Annie Moriondo.

## License

Instructional material from this lesson is made available under the
[Creative Commons Attribution][cc-by-human] ([CC BY 4.0][cc-by-legal]) license. Except where
otherwise noted, example programs and software included as part of this lesson are made available
under the [MIT license][mit-license]. For more information, see [LICENSE.md](LICENSE.md).

[sw-python]: https://swcarpentry.github.io/python-novice-inflammation/
[sw-site]: https://software-carpentry.org/
[best-practices]: https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1001745
[good-practices]: https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1005510
[R]: https://github.com/swcarpentry/r-novice-inflammation
[MATLAB]: https://github.com/swcarpentry/matlab-novice-inflammation
[episode01]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//01-intro/index.html
[episode02]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//02-numpy/index.html
[episode03]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//03-matplotlib/index.html
[episode04]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//04-lists/index.html
[episode05]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//05-loop/index.html
[episode06]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//06-files/index.html
[episode07]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//07-cond/index.html
[episode08]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//08-func/index.html
[episode09]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//09-errors/index.html
[episode10]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//10-defensive/index.html
[episode11]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//11-debugging/index.html
[episode12]: https://broadinstitute.github.io/2024-06-24-python-novice-lesson//12-cmdline/index.html
[cc-by-human]: https://creativecommons.org/licenses/by/4.0/
[cc-by-legal]: https://creativecommons.org/licenses/by/4.0/legalcode
[mit-license]: https://opensource.org/licenses/mit-license.html
