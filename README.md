# Rust RFCs

Many changes, including bug fixes and documentation improvements can be implemented and reviewed via the normal GitHub pull request workflow.

Some changes though are "substantial", and we ask that these be put through a bit of a design process and produce a consensus among the community and the core team.

The "RFC" (request for comments) process is intended to provide a consistent and controlled path for new features to enter the Athena engine and related libraries, so that all stakeholders can be confident about the direction the project is evolving in.

## When you need to follow this process

You need to follow this process if you intend to make "substantial" changes to any project within the athena-org organization, or the RFC process itself.
What constitutes a "substantial" change is evolving based on community norms, but may include the following.

   - Any semantic or syntactic change that is not a bugfix.
   - Removing library features.
   - Adding library features.

Some changes do not require an RFC:

   - Rephrasing, reorganizing, refactoring, or otherwise "changing shape does not change meaning".
   - Additions that strictly improve objective, numerical quality criteria (warning removal, speedup, better platform coverage, more parallelism, trap more errors, etc.)
   - Additions only likely to be _noticed by_ other developers-of-athena, invisible to users-of-athena.

If you submit a pull request to implement a new feature without going through the RFC process, it may be closed with a polite request to submit an RFC first.

*RFC Process and README.md based on [Rust's RFC repository](https://github.com/rust-lang/rfcs)*
