# gittuf/ci-demo

![gittuf Verification](https://github.com/gittuf/ci-demo/actions/workflows/verify.yml/badge.svg)

**NOTE:** This demo is being archived as CI verification is now used more
commonly, including in the [gittuf/gittuf
repository](https://github.com/gittuf/gittuf/blob/d878e5352924d63a0349357b77fa1161d123ef17/.github/workflows/gittuf-verify.yml).

This is a demonstration of using gittuf verification in a CI workflow. This
repository has a simple policy protecting the `main` branch that says all
updates to the branch's state must be signed using Sigstore. The expected
identity is @adityasaky's and the expected issuer is GitHub.

The folder `.keys` includes the root and targets keys used to manage the gittuf
policy.

## Active Policy

The policy on this repository declares the Sigstore identity and a protection
rule applicable to the main branch granting permission to that Sigstore
identity. To inspect the policy in more detail, use `gittuf clone` to download
the repository with the gittuf namespaces. You can find pre-built (and signed)
binaries for gittuf from its latest
[release](https://github.com/gittuf/gittuf/releases). Alternatively, clone the
repository using Git and fetch `refs/gittuf/reference-state-log` and
`refs/gittuf/policy` manually.

```jsonc
{
    "keys": {
        "aditya@saky.in::https://github.com/login/oauth": {
            "keyid_hash_algorithms": null,
            "keytype": "sigstore-oidc",
            "keyval": {
                "identity": "aditya@saky.in",
                "issuer": "https://github.com/login/oauth"
            },
            "scheme": "fulcio",
            "keyid": "aditya@saky.in::https://github.com/login/oauth"
        }
    },
    "roles": [
        {
            "name": "protect-main",
            "paths": [
                "git:refs/heads/main"
            ],
            "terminating": false,
            "keyids": [
                "aditya@saky.in::https://github.com/login/oauth"
            ],
            "threshold": 1
        },
        {
            "name": "gittuf-allow-rule",
            "paths": [
                "*"
            ],
            "terminating": true,
            "keyids": [],
            "threshold": 1
        }
    ]
}
```
