# gittuf/ci-demo

This is a demonstration of using gittuf verification in a CI workflow. This
repository has a simple policy protecting the `main` branch that says all
updates to the branch's state must be signed using Sigstore. The expected
identity is @adityasaky's and the expected issuer is GitHub.

The folder `.keys` includes the root and targets keys used to manage the gittuf
policy.
