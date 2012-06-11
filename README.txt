git-scan-history

A tool to help gather statistics on a git repository.


USAGE

  git-scan-history <range>

Counts the amount of Ruby code for each commit in a range.  Stores the
results using `git notes` so you can push the results to other repositories,
and the results are kept around for resuming interrupted runs.


EXAMPLES

  git-cloc-ruby-sql-notes --first-parent HEAD~100...


FUTURE PLANS

The statistic collection should definitely be user-supplied. `cloc` is
great, but it's really just one example of the kind of stats that are
interesting to collect.

For big codebases where you just want a quick taste of the full stats,
it'd be nice if git-scan-history was clever about the order it
gathered.  Instead of collecting stats in a strictly linear fashion,
it'd be nice to take samples from all over the repository.


BUGS

All kinds. It was originally written as an inline email for
demonstration purposes, so it's growing error handling. It's entirely
possible this tool will mess up your whole repository!


AUTHOR

Rob Hunter <rhunter@thoughtworks.com> is the dang fool who started
reconstructing some analysis he'd done with Flog in a browser email.

