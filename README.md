# Notes on Secrets

This is a list of two things: (1) security incidents that involved exposed secrets, and (2) security research on secret detection.

- 2024-07-08: [Researchers at JFrog find a privileged GitHub access token for the PyPI, Python, and Python Software Foundation organizations](https://jfrog.com/blog/leaked-pypi-secret-token-revealed-in-binary-preventing-suppy-chain-attack/).

  The token was found within a Python bytecode file (a .pyc file) and did not correspond to what was included in source code.
  More details are shared on the [PyPI blog](https://blog.pypi.org/posts/2024-07-08-incident-report-leaked-admin-personal-access-token/).

- 2024-06-23: [Phantom Secrets: Undetected Secrets Expose Major Corporations](https://www.aquasec.com/blog/undetected-hard-code-secrets-expose-corporations/)

  Yakir Kadkoda and Ilay Goldman of Aqua Security investigate how to find additional content in Git repositories that are missed when you do a simple `git clone`.
  As part of this research they demonstrate several cases of real secrets that they found that had been missed previously, which allowed unintended access to several systems.

- 2024-04-15: [50k smart locks from Chirp Systems vulnerable to remote unlock using hardcoded credentials](https://krebsonsecurity.com/2024/04/crickets-from-chirp-systems-in-smart-lock-key-leak/)

- 2024-04-14: [Finding secrets in "lost" commits on GitLab](https://tales.fromprod.com/2024/056/gitlab-secrets.html)

  Richard Finlay Tweed discovered that by viewing GitLab's Events API, you can discover "lost" commit hashes from force push events, and with that, recover the content.

  A code implementation of the idea is available as [a project on GitHub](https://github.com/RichardoC/gitlab-secrets).

- 2024-04-09: [Microsoft exposes passwords in inadvertently exposed Azure storage bucket](https://techcrunch.com/2024/04/09/microsoft-employees-exposed-internal-passwords-security-lapse/)

- 2024-04-01: [Samsung inadvertently exposes a privileged GitHub Enterprise token in a Jenkins instance that was unintentionally exposed to the Internet](https://maia.crimew.gay/posts/i-hacked-samsung/)

- 2024-03-24: [Ultimate guide to secrets in Lambda](https://aaronstuyvenberg.com/posts/ultimate-lambda-secrets-guide)

  AJ Stuyvenberg shares a detailed guide on various approaches to dealing with secrets in AWS Lambda.

- 2024-03-19: [Misconfigured Firebase instances leak 19 million plaintext passwords](https://www.bleepingcomputer.com/news/security/misconfigured-firebase-instances-leaked-19-million-plaintext-passwords/)

- 2024-03-07: [Private links discovered to be publicly exposed in multiple URL-scanning services](https://vin01.github.io/piptagole/security-tools/soar/urlscan/hybrid-analysis/data-leaks/urlscan.io/cloudflare-radar%22/2024/03/07/url-database-leaks-private-urls.html)

- 2024-02-29: [GitHub enables by default the blocking of pushes containing hardcoded credentials in public repositories](https://github.blog/2024-02-29-keeping-secrets-out-of-public-repositories/)

- 2024-02-29: [GitLab releases an open-source tool to detect secrets exposed in videos](https://gitlab.com/gitlab-com/gl-security/security-research/video-scanner/youtube-video-scanner)

  The tool, [available on GitLab](https://gitlab.com/gitlab-com/gl-security/security-research/video-scanner/youtube-video-scanner), runs an OCR system on each frame of a video, then performs approximate regex matching to detect secrets while accounting for errors in the OCR process.

- 2024-02-21: [TruffleHog now avoids triggering known AWS Canary Tokens when performing credential validation](https://trufflesecurity.com/blog/canaries)

- 2024-02-17: [BMW exposes secret access keys and internal data via Azure bucket misconfiguration.](https://techcrunch.com/2024/02/14/bmw-security-lapse-exposed-sensitive-company-information-researcher-finds/)

- 2024-02-01: [Football Australia hardcodes AWS keypairs into its HTML source, granting access to 127 S3 buckets containing PII, source code, and other non-public data](https://cybernews.com/security/football-australia-leak-expose-players/)

- 2024-01-30: [Twilio Segment integrates with secret scanning from GitHub, GitLab, and others](https://segment.com/blog/how-segment-proactively-protects-customer-api-tokens/)

- 2024-01-26: [Mercedes-Benz inadvertently exposes a privileged GitHub Enterprise token in a public GitHub repository](https://techcrunch.com/2024/01/26/mercedez-benz-token-exposed-source-code-github/)

  This was also [discussed on Hacker News](https://news.ycombinator.com/item?id=39187749).

- 2024-01-17: [Microsoft credentials for Toyota Tsusho Insurance Broker India leaked via insurance calculator website](https://eaton-works.com/2024/01/17/ttibi-email-hack/)

  A security researcher at [Eaton](https://eaton-works.com/) found exposed Microsoft credentials for Toyota Tsusho Insurance Broker India on an insurance calculator website for Eicher Motors.
  The insurance calculator website allowed _anyone_ to have it send an email.
  When this functionality was exploited, the HTTP response included server error log messages that exposed additional credentials.
  The researcher was able to access the sending email account, and found all previous emails that had been sent, comprising more than 25GiB of sensitive data.

- 2023-12-04: [Cyber Av3ngers gang hacks industrial controllers across multiple US states](https://www.scmagazine.com/news/cyber-av3ngers-gang-hacks-industrial-controllers-across-multiple-us-states)

  An Iranian threat group hacked into a Pennsylvanian water authority pump station controller, Pittsburgh’s Full Pint Beer brewery, 4 other utilities, and a public aquarium.
  The targets involved Unitronics PLCs, which were compromised using the default port (20256) and credentials (`1111`).

- 2023-12-04: Bar Lanyado from Lasso Security [found more than 1500 valid exposed HuggingFace API tokens](https://www.lasso.security/blog/1500-huggingface-api-tokens-were-exposed-leaving-millions-of-meta-llama-bloom-and-pythia-users-for-supply-chain-attacks) using the search functionality on GitHub and HuggingFace

  Some of the tokens had write permission, including to high-profile models including [Bloom](https://bigscience.huggingface.co/blog/bloom), [Meta-Llama](https://ai.meta.com/llama/), and [Pythia](https://github.com/EleutherAI/pythia).
  These leaked credentials could be used for several supply chain attacks, including backdooring models, poisoning training data, and stealing confidential models and data.
  This was additionally covered [here](https://www.darkreading.com/vulnerabilities-threats/meta-ai-models-cracked-open-exposed-api-tokens).

- 2023-12-04: GitHub [now scans discussions for secrets](https://github.blog/changelog/2023-12-04-secret-scanning-now-detects-new-secrets-in-github-discussion-content/)

  This is an extension on their earlier changes to [scan issues for secrets](https://github.blog/changelog/2023-08-16-secret-scanning-detects-secrets-in-issues-for-free-public-repositories/).

- 2023-11-21: [The Ticking Supply Chain Attack Bomb of Exposed Kubernetes Secrets](https://blog.aquasec.com/the-ticking-supply-chain-attack-bomb-of-exposed-kubernetes-secrets)

  Yakir Kadkoda and Assaf Morag of Aqua Security describe finding numerous valid credentials for Kubernetes clusters in public GitHub repositories.
  Such secrets go undetected by other tools, probably because they are base64-encoded in YAML files by default.

- 2023-11-14: [All the Small Things: Azure CLI Leakage and Problematic Usage Patterns](https://www.paloaltonetworks.com/blog/prisma-cloud/secrets-leakage-user-error-azure-cli/)

  Aviad Hahami of Palo Alto Networks writes up some simple but high-impact secret exposure vulnerabilities in GitHub Actions when using the `azure/login` action.
  That action would leak the environment to the build log in certain cases, making secrets visible to anyone who would look at the log.

- 2023-11-13: [Uncovering thousands of unique secrets in PyPI packages](https://blog.gitguardian.com/uncovering-thousands-of-unique-secrets-in-pypi-packages/)

  Tom Forbes follow up on his earlier independent research on [finding AWS keys in PyPI packages](https://tomforb.es/i-scanned-every-package-on-pypi-and-found-57-live-aws-keys/), this time with GitGuardian, and found 768 provably live secrets.

- 2023-11-08: GitHub offers an [LLM-powered secrets scanner](https://github.blog/changelog/2023-11-08-secret-scanning-detects-generic-passwords-with-ai-limited-beta/) with its Advanced Security package, currently in beta

- 2023-11-08: GitHub offers a [generative AI-powered regex generator](https://github.blog/changelog/2023-11-08-generate-custom-patterns-for-secret-scanning-with-ai/) with its Advanced Security package, currently in beta

- 2023-10-26: GitHub [scans NPM packages for exposed secrets](https://github.blog/changelog/2023-10-26-secret-scanning-scans-public-npm-packages/)

- 2023-08-17: PyPI is a GitHub Secrets Scanning partner, and [automatically revokes exposed PyPI tokens](https://blog.pypi.org/posts/2023-08-17-github-token-scanning-for-public-repos/) that are found

  In 15 months, PyPI has revoked over 500 exposed tokens.

- 2023-01-06: [I scanned every package on PyPi and found 57 live AWS keys](https://tomforb.es/i-scanned-every-package-on-pypi-and-found-57-live-aws-keys/)

  [Tom Forbes](https://tomforb.es) scanned every PyPI package for AWS keys, tested each one for validity, and found 57 live keys.
  Cleverly, the automation that he wrote runs in GitHub Actions, and automatically commits any found valid keypair to a public GitHub repository, causing the AWS/GitHub secret scanning integration to invalidate those credentials.
  This is a bold move, as it could break live applications.
  He [released the application](https://github.com/pypi-data/pypi-aws-secrets) that runs in GitHub Actions under the MIT license.
  Additionally, here [released another repository](https://github.com/pypi-data/pypi-json-data) that has the contents of the PyPI JSON API for all packages, updated every 12 hours.
  This could be a useful launch point for other people investigating PyPI in bulk.
