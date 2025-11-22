# Notes on Secrets

This is a list of two things: (1) security incidents that involved exposed secrets, and (2) security research on secret detection.

- 2025-11-19: [Secret detectors miss many real secrets due to false positive mitigations](https://semgrep.dev/blog/2025/secrets-story-and-prefixed-secrets/)

  Lewis Ardern from Semgrep details a number of cases where the false positive mitigations that secret detectors use cause them to miss live secrets.
  In particular, regular expressions that require nearby keywords or non-word-character anchors are significant culprits.
  Many of the secrets they found were exposed in public GitHub repositories, and found by no popular tool that they tried, including GitHub's own secret scanning.

- 2025-10-29: [Ernst & Young accidentally expose secrets in 4TB database backup file](https://www.neosecurity.nl/blog/ey-data-leak-4tb-sql-server-backup)

  Researchers at Neo Security came across a 4TB SQL Server backup file in an Azure storage bucket.
  Through some investigation they discovered that the bucket belonged to Ernst & Young, and that it contained secrets.

- 2025-10-28: [Tata Motors leaks AWS keys granting access to 70TB of data](https://eaton-works.com/2025/10/28/tata-motors-hack/)

  Eaton Zveare discovered two AWS keys in the frontend Typescript code for a parts ordering website of Tata Motors.
  The keys granted access to hundreds of S3 buckets containing 70TB of sensitive information, including customer lists and invoices.

- 2025-07-31: [Finding secrets with a combination of regex and a fine-tuned BERT-based model](https://specterops.io/blog/2025/07/31/whats-your-secret-secret-scanning-by-deeppass2/)

  SpecterOps shares details of DeepPass2, their second iteration of a system designed to detect hardcoded secrets, particularly freeform passwords.
  DeepPass2 combines regex-based secrets detection from [Nosey Parker](https://github.com/praetorian-inc/noseyparker) with a custom fine-tuned BERT-based language model (xlm-RoBERTa-base).

- 2025-06-10: [Lean and Mean: How We Fine-Tuned a Small Language Model for Secret Detection in Code](https://www.wiz.io/blog/small-language-model-for-secrets-detection-in-code)

  Erez Harush and Daniel Lazarev of Wiz give details of a "small" language model (Llama 3.2 1B) that they fine-tuned for generic secrets detection.
  They note that secret detection using big hosted LLMs would be time- and cost-prohibitive at realistic scale.
  They share some details of their training data preparation: they used public files from GitHub, eliminated near duplicates, and used an ensemble of LLMs to detect and label likely secrets from within those files.
  Their end result is a smaller secrets detection model that can run in a few seconds per file on a regular CPU, and scores >80% on both precision and recall.

- 2025-04-22: [How I made $64k from deleted files — a bug bounty story](https://medium.com/@sharon.brizinov/how-i-made-64k-from-deleted-files-a-bug-bounty-story-c5bd3a6f5f9b)

  Sharon Brizinov details how he ran a secrets detection campaign at scale against numerous bug bounty programs, netting $64k.
  His insight was to scan files in Git history that had been deleted, and were not readily accessible unless you went out of your way looking for them.

- 2024-10-29: [Partial passwords for Colorado voting systems accidentally exposed in spreadsheet of Department of State website](https://www.sos.state.co.us/pubs/newsRoom/pressReleases/2024/PR20241029Passwords.html).

- 2024-10-20: [Internet Archive compromised after hackers discover hardcoded Zendesk credentials in GitLab repositories](https://www.bleepingcomputer.com/news/security/internet-archive-breached-again-through-stolen-access-tokens/).

  A hacker found an exposed GitLab configuration file that included Git credentials, allowing them to access non-public source code, which included additional credentials.
  These credentials included Zendesk support system credentials that exposed more than 800k support tickets.
  This is the second time in October that the Internet Archive was hacked.

- 2024-08-15: [Palo Alto Network's Unit 42 researchers discover extortion campaign that gains initial access to victim networks by finding exposed secrets in accidentally exposed `.env` files](https://unit42.paloaltonetworks.com/large-scale-cloud-extortion-operation/).

- 2024-08-08: [What's the worst place to leave your secrets? Research into what happens to AWS credentials that are left in public places](https://cybenari.com/2024/08/whats-the-worst-place-to-leave-your-secrets/).

  Idan Ben Ari at Cybernari use canary tokens to investigate how quickly tokens are detected and used when placed in various public places.
  The places include GitHub, GitLab, Bitbucket, DockerHub, HTTP servers, FTP servers, Pastebin, JSFiddle, PyPI, npm, S3, and GCS.
  Half the tokens were compromised, sometimes within seconds or minutes of publishing, though some places averaged days before compromise.

- 2024-07-24: [American Megatrends International leaks its Secure Boot platform key in a public GitHub repository, affecting over 900 models](https://www.binarly.io/blog/pkfail-untrusted-platform-keys-undermine-secure-boot-on-uefi-ecosystem).

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
