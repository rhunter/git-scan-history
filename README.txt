git-scan-history

A tool to help gather statistics on a git repository.


USAGE

  git-scan-history --run <collection script> [options] <range>

Runs a command for each commit in a range.  Stores the results using
`git notes` so you can push the results to other repositories,
and the results are kept around for resuming interrupted runs.


USING THE RESULTS

The results are stored in `git notes` (by default, in the `scan-history`
namespace, which is to say `refs/notes/scan-history`).

You can use the `git notes` command to show commits with statistics:

    $ git notes --notes-ref ref/notes/scan-history list
    d1cd03e62d4c418ada81faaa0496df4b11d2b8e8 02d86ac992007aa0454e7c161233c2b271c9fb88
    b4928b0cdd1014166bdb220cac37d05f1b200f82 31d831328c06ba13563496573b3c999781927010
    9cb93bdc26b58328ee1b23296b8dcd3a599b8035 42aa6615b23234a3b2b4716c827362b4f5057986
    ada9f9fd916aa60b61280900008976bb6253b99b 87abb6cf0f7f4178907d55475390e6b8b4c9124e

Each note hash is listed alongside the commit that it annotates. The
notes will show up in `git log` if you want:

    $ GIT_NOTES_REF=refs/notes/scan-history git log

You can push them to a remote repository:

    $ git push origin refs/notes/scan-history

Perhaps your 'command' is in a combinable format like SQL INSERT statements:

    $ git archive refs/notes/scan-history | tar xO | sqlite3 mydb.sqlite3

Since notes are stored as plain old git blobs, you can also get at them
directly:

    $ git cat-file blob 87abb6cf0f7f4178907d55475390e6b8b4c9124e
    $ git cat-file blob 87abb6cf0f7f4178907d55475390e6b8b4c9124e



EXAMPLES

  git scan-history --script 'cloc .' --sample-every 5 --first-parent HEAD~100...



FUTURE PLANS

For big codebases where you just want a quick taste of the full stats,
it'd be nice if git-scan-history was clever about the order it
gathered.  Instead of collecting stats in a strictly linear fashion,
it'd be nice to take samples from all over the repository.


BUGS

All kinds. It was originally written as an inline email for
demonstration purposes, so it's growing error handling. It's entirely
possible this tool will mess up your whole repository!

Notably, any error in the script will probably cause poor results.

AUTHOR

Rob Hunter <rhunter@thoughtworks.com> is the dang fool who started
reconstructing some analysis he'd done with Flog in a browser email.

