# eyeful-demo

Pull requests that [eyeful](https://github.com/Pleasurecruise/eyeful) reviews in GitHub Actions,
one case per public benchmark task. Each case reintroduces a real bug, so a review can be checked
against what is known to be wrong.

Each case is a pair of branches named after its task, built on the upstream project's own history:

- `<case>/base`: the upstream commit the task starts from, then the task's reference fix without its
  tests, then the environment the benchmark pins, so eyeful's sandbox can install and test it;
- `<case>/change`: one commit that reverts the fix.

The pull request goes from `<case>/change` into `<case>/base`. eyeful reviews it when it is opened,
and again on a `/eyeful` comment. Only `main` holds the workflow, and the review never sees this README.

| Case | Source | Bug | Pull request |
| --- | --- | --- | --- |
| `pallets__flask-5014` | [SWE-bench Verified](https://huggingface.co/datasets/princeton-nlp/SWE-bench_Verified) | [pallets/flask#5014](https://github.com/pallets/flask/issues/5014): a Blueprint accepts an empty name | [#1](https://github.com/Pleasurecruise/eyeful-demo/pull/1) |
| `psf__requests-5414` | [SWE-bench Verified](https://huggingface.co/datasets/princeton-nlp/SWE-bench_Verified) | [psf/requests#5414](https://github.com/psf/requests/pull/5414): `http://.example.com` raises `UnicodeError` instead of `InvalidURL` | |
