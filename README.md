# eyeful-demo

Pull requests that [eyeful](https://github.com/Pleasurecruise/eyeful) reviews in GitHub Actions,
one case per public benchmark task. Each case reintroduces a real bug, so a review can be checked
against what is known to be wrong.

Each case is a pair of branches named after its task, built on the upstream project's own history:

- `<case>/base`: the upstream commit the task starts from, then the environment the benchmark pins,
  so eyeful's sandbox can install and test it. `.github/eyeful.yml` there declares the project's
  commands. In a bug case the task's reference fix, without its tests, comes before the
  environment;
- `<case>/change`: in a bug case, one commit that reverts the fix; in a clean case, the reference
  fix with its tests, which should draw no issue.

The pull request goes from `<case>/change` into `<case>/base`. eyeful reviews it when it is opened,
and again on a `/eyeful` comment. Only `main` holds the workflow, and the review never sees this README.

The cases come from projects that eyeful's evaluation does not sample, so tuning on them cannot leak
into its results.

| Case | Source | What the pull request does | Pull request |
| --- | --- | --- | --- |
| `sympy__sympy-24443` | [SWE-bench Verified](https://huggingface.co/datasets/princeton-nlp/SWE-bench_Verified) | Bug: `homomorphism` between permutation groups raises `ValueError` for valid images ([sympy/sympy#24443](https://github.com/sympy/sympy/pull/24443)) | [#3](https://github.com/Pleasurecruise/eyeful-demo/pull/3) |
| `sympy__sympy-18199` | [SWE-bench Verified](https://huggingface.co/datasets/princeton-nlp/SWE-bench_Verified) | Bug: `nthroot_mod` misses the root 0 and fails on composite moduli ([sympy/sympy#18199](https://github.com/sympy/sympy/pull/18199)) | [#4](https://github.com/Pleasurecruise/eyeful-demo/pull/4) |
| `sympy__sympy-13091` | [SWE-bench Verified](https://huggingface.co/datasets/princeton-nlp/SWE-bench_Verified) | Clean: comparisons return `NotImplemented` for unknown types, across 21 files ([sympy/sympy#13091](https://github.com/sympy/sympy/pull/13091)) | [#5](https://github.com/Pleasurecruise/eyeful-demo/pull/5) |
