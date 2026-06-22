# Contributing to bigmelon

Thank you for your interest in contributing to `bigmelon`.

This project is an R/Bioconductor-style package for memory-efficient DNA methylation pre-processing and analysis.

Because this package is distributed through Bioconductor, all contributions must follow both Bioconductor policies and standard R package development practices. This guide outlines the conventions used in the codebase and explains how to contribute code, documentation, tests, and bug reports in a consistent, review‑friendly way. We assume you are familiar with using Git for collaborative development; if not, we recommend starting with an [introductory Git tutorial](https://coding-for-reproducible-research.github.io/CfRR_Courses/individual_modules/section_landing_pages/introduction_to_version_control.html) before contributing.


## Quick start: Making changes to the codebase

1. **Open an Issue** describing the bug you plan to fix or the feature you want to add, and assign it to yourself.
2. **Create a feature branch** by cloning the repository and branching from `master`. When opening an issue, you can choose to auto‑create a branch linked to it.
3. **Implement your changes** on the feature branch.
4. **Add tests** to cover new functionality or verify bug fixes.
5. **Update documentation** for any new functions or modify existing docs as needed.
6. **Open a pull request** with a concise summary of the problem, the changes made, and how to test them.
7. **Undergo review** by another developer, who may approve the PR or request additional changes.
8. **Merge:** once approved, your PR will be merged into `master`.
9. **Clean up** by closing the issue and deleting your feature branch.

## How can I get involved?

We welcome contributions of all kinds—no prior experience is needed. Here is a non-exhaustive list of simple ways to get involved, all of which help improve the package:

**Report issues:** If you spot a bug or something that doesn’t work as expected, open an issue and describe the problem.
**Suggest improvements:** Ideas for new features or enhancements are always welcome—just submit them as issues.
**Fix bugs you find:** If you’re able to, try fixing an issue you’ve encountered and submit a pull request.
**Help with existing issues:** Browse open issues to find bugs reported by others—many are tagged to help beginners get started.


## Reporting bugs

If you encounter a bug, please report it using GitHub Issues to help us track and resolve problems efficiently.

Before opening a new issue, check the existing issues to see if the problem has already been reported. If it has, you can add relevant details or 👍 react to show it affects you too.

When creating a bug report, please include:

* A clear, descriptive title summarizing the issue
* Steps to reproduce the problem (as detailed and minimal as possible)
* Expected behavior (what you think should happen)
* Actual behavior (what actually happens, including error messages)
* Environment details such as OS, version numbers, or dependencies
* Screenshots or logs if applicable

Clear and detailed reports help us fix issues faster. This same process can also be used to request new features, functions or enhancements. 

## Developer environment

R provides several tools and packages that help automate and streamline package development. To keep the workflow as simple and reliable as possible, we recommend the following setup and development environment.

#### Recommended tools
* R
* Rstudio 
* All `suggests` packages in `DESCRIPTION`
* developer helpers
```
install.packages(c("devtools", "roxygen2"))
```

#### Recommended workflow
After making changes use `devtools` to run checks

```
devtools::load_all()
devtools::test()
devtools::check()

```

You may wish to review a [tutorial on how to build R packages](https://r-pkgs.org/introduction.html), to better understand the typical development workflow, structure, and tools used for building R packages.

## Repository structure

- `R/`: main R source files
- `man/`: Rd documentation files for exported functions
- `tests/runTests.R`: package-level test runner
- `inst/unitTests/`: lower-level internal and user-facing tests
- `data/`: rdata objects that the package loads internally
- `vignettes/`: source files for vignettes
- `README.md`: project overview and installation instructions
- `DESCRIPTION`, `NAMESPACE`: package metadata and exports

## Coding conventions

### R style

- Use `<-` for assignment.
- Use `=` for named function arguments and calls.
- Prefer full logical constants `TRUE`, `FALSE`, and `NULL`.
- Use lower-case function names with dot notation for word separation, e.g. `db.gdsn`, `pfilter.gds`, `prcomp.gds.class`.
- Keep variable names descriptive and lower-case. Short helper names are acceptable inside dense algorithms.

### Formatting

- Use 4-space indent for blocks.
- Align multiline function arguments and calls neatly.
- Keep code readable with spaces around operators and after commas.
- Use comment blocks with `#`, and section markers such as `# {{{` / `# }}}` can be used for long code regions.

### Comments and documentation

- Document exported functions with Roxygen-style comments where appropriate (`#' ...`).
- Keep inline comments focused and explain why code exists, not just what it does.
- Maintain or improve corresponding documentation in `man/` if adding or changing exported behavior.

### Function design

- Define functions in `R/`.
- For internal helpers, a leading dot prefix is used e.g. `.getEstimate2`.
- Use `stopifnot()`, `stop()`, and `message()` for validation and informative errors.
- Keep functions focused on a single task when possible.

### Package conventions

- This package is structured for Bioconductor-style development.
- `R/zzz.R` contains package load-time behavior.
- Many functions implement methods for `gds.class` and `gdsn.class` objects, including S3/S4 style definitions.
- Keep exported methods consistent with existing class/method naming patterns.

## Testing

- Add or update tests in `inst/unitTests/test_user.R` or `inst/unitTests/test_internal.R`.
- Use `tests/runTests.R` to exercise the package tests.
- Ensure new features and bug fixes are covered by tests.
- Keep tests deterministic and avoid writing tests that depend on external network resources.

## Documentation

- Update `README.md` only for user-facing installation or usage changes.
- Keep documentation clear, accurate, and consistent with the code.

This package currently contains a mix of manually written .Rd files and functions documented using **roxygen2** (identified by #' comment blocks above the function). When modifying functions that do not use roxygen2, you must update the corresponding `man/*.Rd` files to reflect any changes in arguments or behaviour. Alternatively, you may convert the function to use roxygen2, which we encourage.

For all **new functions**, we recommend using **roxygen2 with Markdown enabled**. When documenting with roxygen2:
* Include examples that run quickly and reproducibly.
* Document all arguments, return values, and any side effects.
* Follow Bioconductor‑style conventions for documenting S4 classes and methods.

Once roxygen comments are in place, regenerate documentation with:

```
devtools::document()
```



## Submitting changes

- Ensure your branch is up-to-date with `master` before opening a pull request.
- Provide a short summary of the change, the reason for it, and any testing performed.
- Link related issues if available.
- Keep changes small and reviewable when possible.

## Notes

- The codebase does not enforce a strict automatic formatter, so follow the existing dominant patterns in the package.
- If you introduce new helper functions or methods, keep them consistent with the repository’s naming and style conventions.
- Try to preserve the current codebase style while improving readability and maintainability.

## Bioconductor-specific requirements

Bioconductor has strict policies. Contributions must follow:

#### Package structure
* Use S4 classes where appropriate
* Export only necessary functions
* Use @importFrom rather than @import
* Avoid non‑standard evaluation unless documented

#### Dependencies
* Prefer Bioconductor packages over CRAN equivalents
* Avoid heavy dependencies
* Use Suggests: for optional features

#### Performance
* Avoid slow operations inside loops
* Use vectorised operations or apply‑family functions

#### Reproducibility
* Examples and vignettes must run quickly
* No external internet access
* No random results without set.seed()

#### R CMD check
Bioconductor requires:
* No ERRORs
* No WARNINGs
* Minimal NOTEs (preferably none)

## Contributor recognition
All meaningful contributions will be acknowledged in:
* DESCRIPTION (Authors@R)
* NEWS.md
* Release notes

We value contributions of all kinds — code, documentation, testing, and discussion.

## Questions
If you’re unsure about anything, open an issue. We’re happy to help guide contributions so they meet Bioconductor standards.
