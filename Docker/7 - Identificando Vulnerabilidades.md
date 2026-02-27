
No mercado temos algumas soluções para scan de imagens. Aqui iremos comentar algumas delas.
### Trivy

A solução pode ser baixada através do https://trivy.dev/ . Após instalação, o comando é reconhecido, conforme exemplo:

```
$ admin@jupiter:~/giropops-senhas$ trivy --help
Scanner for vulnerabilities in container images, file systems, and Git repositories, as well as for configuration issues and hard-coded secrets

Usage:
  trivy [global flags] command [flags] target
  trivy [command]

Examples:
  # Scan a container image
  $ trivy image python:3.4-alpine
  
  ...
```

Então, é possível realizamos um scan nas imagens que possuímos localmente:

```
$ trivy image giropops-senha:2.0
2026-02-26T07:04:54Z	INFO	[vuln] Vulnerability scanning is enabled
2026-02-26T07:04:54Z	INFO	[secret] Secret scanning is enabled
2026-02-26T07:04:54Z	INFO	[secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2026-02-26T07:04:54Z	INFO	[secret] Please see https://trivy.dev/docs/v0.69/guide/scanner/secret#recommendation for faster secret detection
2026-02-26T07:04:57Z	INFO	[python] Licenses acquired from one or more METADATA files may be subject to additional terms. Use `--debug` flag to see all affected packages.
2026-02-26T07:04:57Z	INFO	Detected OS	family="debian" version="13.3"
2026-02-26T07:04:57Z	INFO	[debian] Detecting vulnerabilities...	os_version="13" pkg_num=87
2026-02-26T07:04:57Z	INFO	Number of language-specific files	num=1
2026-02-26T07:04:57Z	INFO	[python-pkg] Detecting vulnerabilities...
2026-02-26T07:04:57Z	WARN	Using severities from other vendors for some vulnerabilities. Read https://trivy.dev/docs/v0.69/guide/scanner/vulnerability#severity-selection for details.
2026-02-26T07:04:57Z	INFO	Table result includes only package filenames. Use '--format json' option to get the full path to the package file.

Report Summary

┌──────────────────────────────────────────────────────────────────────────────────┬────────────┬─────────────────┬─────────┐
│                                      Target                                      │    Type    │ Vulnerabilities │ Secrets │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ giropops-senha:2.0 (debian 13.3)                                                 │   debian   │       68        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/async_timeout-5.0.1.dist-info/METADATA    │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/blinker-1.9.0.dist-info/METADATA          │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/click-8.3.1.dist-info/METADATA            │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/flask-3.0.3.dist-info/METADATA            │ python-pkg │        1        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/itsdangerous-2.2.0.dist-info/METADATA     │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/jinja2-3.1.6.dist-info/METADATA           │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/markupsafe-3.0.3.dist-info/METADATA       │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/pip-24.0.dist-info/METADATA               │ python-pkg │        2        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/prometheus_client-0.16.0.dist-info/METAD- │ python-pkg │        0        │    -    │
│ ATA                                                                              │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/redis-4.5.4.dist-info/METADATA            │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools-79.0.1.dist-info/METADATA      │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/autocommand-2.2.2.dis- │ python-pkg │        0        │    -    │
│ t-info/METADATA                                                                  │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/backports.tarfile-1.2- │ python-pkg │        0        │    -    │
│ .0.dist-info/METADATA                                                            │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/importlib_metadata-8.- │ python-pkg │        0        │    -    │
│ 0.0.dist-info/METADATA                                                           │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/inflect-7.3.1.dist-in- │ python-pkg │        0        │    -    │
│ fo/METADATA                                                                      │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/jaraco.collections-5.- │ python-pkg │        0        │    -    │
│ 1.0.dist-info/METADATA                                                           │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/jaraco.context-5.3.0.- │ python-pkg │        1        │    -    │
│ dist-info/METADATA                                                               │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/jaraco.functools-4.0.- │ python-pkg │        0        │    -    │
│ 1.dist-info/METADATA                                                             │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/jaraco.text-3.12.1.di- │ python-pkg │        0        │    -    │
│ st-info/METADATA                                                                 │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/more_itertools-10.3.0- │ python-pkg │        0        │    -    │
│ .dist-info/METADATA                                                              │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/packaging-24.2.dist-i- │ python-pkg │        0        │    -    │
│ nfo/METADATA                                                                     │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/platformdirs-4.2.2.di- │ python-pkg │        0        │    -    │
│ st-info/METADATA                                                                 │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/tomli-2.0.1.dist-info- │ python-pkg │        0        │    -    │
│ /METADATA                                                                        │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/typeguard-4.3.0.dist-- │ python-pkg │        0        │    -    │
│ info/METADATA                                                                    │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/typing_extensions-4.1- │ python-pkg │        0        │    -    │
│ 2.2.dist-info/METADATA                                                           │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/wheel-0.45.1.dist-inf- │ python-pkg │        1        │    -    │
│ o/METADATA                                                                       │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/setuptools/_vendor/zipp-3.19.2.dist-info- │ python-pkg │        0        │    -    │
│ /METADATA                                                                        │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/werkzeug-3.1.6.dist-info/METADATA         │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ usr/local/lib/python3.11/site-packages/wheel-0.45.1.dist-info/METADATA           │ python-pkg │        1        │    -    │
└──────────────────────────────────────────────────────────────────────────────────┴────────────┴─────────────────┴─────────┘
Legend:
- '-': Not scanned
- '0': Clean (no security findings detected)


giropops-senha:2.0 (debian 13.3)

Total: 68 (UNKNOWN: 0, LOW: 51, MEDIUM: 15, HIGH: 2, CRITICAL: 0)

┌────────────────┬─────────────────────┬──────────┬──────────┬─────────────────────────────┬───────────────┬──────────────────────────────────────────────────────────────┐
│    Library     │    Vulnerability    │ Severity │  Status  │      Installed Version      │ Fixed Version │                            Title                             │
├────────────────┼─────────────────────┼──────────┼──────────┼─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ apt            │ CVE-2011-3374       │ LOW      │ affected │ 3.0.3                       │               │ It was found that apt-key in apt, all versions, do not       │
│                │                     │          │          │                             │               │ correctly...                                                 │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2011-3374                    │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ bash           │ TEMP-0841856-B18BAF │          │          │ 5.2.37-2+b7                 │               │ [Privilege escalation possible to other user than root]      │
│                │                     │          │          │                             │               │ https://security-tracker.debian.org/tracker/TEMP-0841856-B1- │
│                │                     │          │          │                             │               │ 8BAF                                                         │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ bsdutils       │ CVE-2025-14104      │ MEDIUM   │          │ 1:2.41-5                    │               │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                │                     │          │          │                             │               │ when processing 256-byte usernames                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2022-0563       │ LOW      │          │                             │               │ util-linux: partial disclosure of arbitrary files in chfn    │
│                │                     │          │          │                             │               │ and chsh when compiled...                                    │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ coreutils      │ CVE-2017-18018      │          │          │ 9.7-3                       │               │ coreutils: race condition vulnerability in chown and chgrp   │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2017-18018                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2025-5278       │          │          │                             │               │ coreutils: Heap Buffer Under-Read in GNU Coreutils sort via  │
│                │                     │          │          │                             │               │ Key Specification                                            │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-5278                    │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libapt-pkg7.0  │ CVE-2011-3374       │          │          │ 3.0.3                       │               │ It was found that apt-key in apt, all versions, do not       │
│                │                     │          │          │                             │               │ correctly...                                                 │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2011-3374                    │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libblkid1      │ CVE-2025-14104      │ MEDIUM   │          │ 2.41-5                      │               │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                │                     │          │          │                             │               │ when processing 256-byte usernames                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2022-0563       │ LOW      │          │                             │               │ util-linux: partial disclosure of arbitrary files in chfn    │
│                │                     │          │          │                             │               │ and chsh when compiled...                                    │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libc-bin       │ CVE-2026-0861       │ HIGH     │          │ 2.41-12+deb13u1             │               │ glibc: Integer overflow in memalign leads to heap corruption │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2026-0861                    │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2025-15281      │ MEDIUM   │          │                             │               │ glibc: wordexp with WRDE_REUSE and WRDE_APPEND may return    │
│                │                     │          │          │                             │               │ uninitialized memory                                         │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-15281                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2026-0915       │          │          │                             │               │ glibc: glibc: Information disclosure via zero-valued network │
│                │                     │          │          │                             │               │ query                                                        │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2026-0915                    │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2010-4756       │ LOW      │          │                             │               │ glibc: glob implementation can cause excessive CPU and       │
│                │                     │          │          │                             │               │ memory consumption due to...                                 │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2010-4756                    │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2018-20796      │          │          │                             │               │ glibc: uncontrolled recursion in function                    │
│                │                     │          │          │                             │               │ check_dst_limits_calc_pos_1 in posix/regexec.c               │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2018-20796                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-1010022    │          │          │                             │               │ glibc: stack guard protection bypass                         │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-1010022                 │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-1010023    │          │          │                             │               │ glibc: running ldd on malicious ELF leads to code execution  │
│                │                     │          │          │                             │               │ because of...                                                │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-1010023                 │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-1010024    │          │          │                             │               │ glibc: ASLR bypass using cache of thread stack and heap      │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-1010024                 │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-1010025    │          │          │                             │               │ glibc: information disclosure of heap addresses of           │
│                │                     │          │          │                             │               │ pthread_created thread                                       │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-1010025                 │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-9192       │          │          │                             │               │ glibc: uncontrolled recursion in function                    │
│                │                     │          │          │                             │               │ check_dst_limits_calc_pos_1 in posix/regexec.c               │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-9192                    │
├────────────────┼─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│ libc6          │ CVE-2026-0861       │ HIGH     │          │                             │               │ glibc: Integer overflow in memalign leads to heap corruption │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2026-0861                    │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2025-15281      │ MEDIUM   │          │                             │               │ glibc: wordexp with WRDE_REUSE and WRDE_APPEND may return    │
│                │                     │          │          │                             │               │ uninitialized memory                                         │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-15281                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2026-0915       │          │          │                             │               │ glibc: glibc: Information disclosure via zero-valued network │
│                │                     │          │          │                             │               │ query                                                        │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2026-0915                    │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2010-4756       │ LOW      │          │                             │               │ glibc: glob implementation can cause excessive CPU and       │
│                │                     │          │          │                             │               │ memory consumption due to...                                 │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2010-4756                    │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2018-20796      │          │          │                             │               │ glibc: uncontrolled recursion in function                    │
│                │                     │          │          │                             │               │ check_dst_limits_calc_pos_1 in posix/regexec.c               │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2018-20796                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-1010022    │          │          │                             │               │ glibc: stack guard protection bypass                         │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-1010022                 │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-1010023    │          │          │                             │               │ glibc: running ldd on malicious ELF leads to code execution  │
│                │                     │          │          │                             │               │ because of...                                                │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-1010023                 │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-1010024    │          │          │                             │               │ glibc: ASLR bypass using cache of thread stack and heap      │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-1010024                 │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-1010025    │          │          │                             │               │ glibc: information disclosure of heap addresses of           │
│                │                     │          │          │                             │               │ pthread_created thread                                       │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-1010025                 │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2019-9192       │          │          │                             │               │ glibc: uncontrolled recursion in function                    │
│                │                     │          │          │                             │               │ check_dst_limits_calc_pos_1 in posix/regexec.c               │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2019-9192                    │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ liblastlog2-2  │ CVE-2025-14104      │ MEDIUM   │          │ 2.41-5                      │               │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                │                     │          │          │                             │               │ when processing 256-byte usernames                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2022-0563       │ LOW      │          │                             │               │ util-linux: partial disclosure of arbitrary files in chfn    │
│                │                     │          │          │                             │               │ and chsh when compiled...                                    │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────┼─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│ libmount1      │ CVE-2025-14104      │ MEDIUM   │          │                             │               │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                │                     │          │          │                             │               │ when processing 256-byte usernames                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2022-0563       │ LOW      │          │                             │               │ util-linux: partial disclosure of arbitrary files in chfn    │
│                │                     │          │          │                             │               │ and chsh when compiled...                                    │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libncursesw6   │ CVE-2025-6141       │          │          │ 6.5+20250216-2              │               │ gnu-ncurses: ncurses Stack Buffer Overflow                   │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-6141                    │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libsmartcols1  │ CVE-2025-14104      │ MEDIUM   │          │ 2.41-5                      │               │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                │                     │          │          │                             │               │ when processing 256-byte usernames                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2022-0563       │ LOW      │          │                             │               │ util-linux: partial disclosure of arbitrary files in chfn    │
│                │                     │          │          │                             │               │ and chsh when compiled...                                    │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libsqlite3-0   │ CVE-2025-7709       │ MEDIUM   │          │ 3.46.1-7                    │               │ An integer overflow exists in the FTS5                       │
│                │                     │          │          │                             │               │ https://sqlite.org/fts5.html e ...                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-7709                    │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2021-45346      │ LOW      │          │                             │               │ sqlite: crafted SQL query allows a malicious user to obtain  │
│                │                     │          │          │                             │               │ sensitive information...                                     │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2021-45346                   │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libsystemd0    │ CVE-2013-4392       │          │          │ 257.9-1~deb13u1             │               │ systemd: TOCTOU race condition when updating file            │
│                │                     │          │          │                             │               │ permissions and SELinux security contexts...                 │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2013-4392                    │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-31437      │          │          │                             │               │ An issue was discovered in systemd 253. An attacker can      │
│                │                     │          │          │                             │               │ modify a...                                                  │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2023-31437                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-31438      │          │          │                             │               │ An issue was discovered in systemd 253. An attacker can      │
│                │                     │          │          │                             │               │ truncate a...                                                │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2023-31438                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-31439      │          │          │                             │               │ An issue was discovered in systemd 253. An attacker can      │
│                │                     │          │          │                             │               │ modify the...                                                │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2023-31439                   │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libtinfo6      │ CVE-2025-6141       │          │          │ 6.5+20250216-2              │               │ gnu-ncurses: ncurses Stack Buffer Overflow                   │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-6141                    │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libudev1       │ CVE-2013-4392       │          │          │ 257.9-1~deb13u1             │               │ systemd: TOCTOU race condition when updating file            │
│                │                     │          │          │                             │               │ permissions and SELinux security contexts...                 │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2013-4392                    │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-31437      │          │          │                             │               │ An issue was discovered in systemd 253. An attacker can      │
│                │                     │          │          │                             │               │ modify a...                                                  │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2023-31437                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-31438      │          │          │                             │               │ An issue was discovered in systemd 253. An attacker can      │
│                │                     │          │          │                             │               │ truncate a...                                                │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2023-31438                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2023-31439      │          │          │                             │               │ An issue was discovered in systemd 253. An attacker can      │
│                │                     │          │          │                             │               │ modify the...                                                │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2023-31439                   │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ libuuid1       │ CVE-2025-14104      │ MEDIUM   │          │ 2.41-5                      │               │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                │                     │          │          │                             │               │ when processing 256-byte usernames                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2022-0563       │ LOW      │          │                             │               │ util-linux: partial disclosure of arbitrary files in chfn    │
│                │                     │          │          │                             │               │ and chsh when compiled...                                    │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ login          │ CVE-2025-14104      │ MEDIUM   │          │ 1:4.16.0-2+really2.41-5     │               │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                │                     │          │          │                             │               │ when processing 256-byte usernames                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2022-0563       │ LOW      │          │                             │               │ util-linux: partial disclosure of arbitrary files in chfn    │
│                │                     │          │          │                             │               │ and chsh when compiled...                                    │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ login.defs     │ CVE-2007-5686       │          │          │ 1:4.17.4-2                  │               │ initscripts in rPath Linux 1 sets insecure permissions for   │
│                │                     │          │          │                             │               │ the /var/lo ......                                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2007-5686                    │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2024-56433      │          │          │                             │               │ shadow-utils: Default subordinate ID configuration in        │
│                │                     │          │          │                             │               │ /etc/login.defs could lead to compromise                     │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2024-56433                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ TEMP-0628843-DBAD28 │          │          │                             │               │ [more related to CVE-2005-4890]                              │
│                │                     │          │          │                             │               │ https://security-tracker.debian.org/tracker/TEMP-0628843-DB- │
│                │                     │          │          │                             │               │ AD28                                                         │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ mount          │ CVE-2025-14104      │ MEDIUM   │          │ 2.41-5                      │               │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                │                     │          │          │                             │               │ when processing 256-byte usernames                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2022-0563       │ LOW      │          │                             │               │ util-linux: partial disclosure of arbitrary files in chfn    │
│                │                     │          │          │                             │               │ and chsh when compiled...                                    │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ ncurses-base   │ CVE-2025-6141       │          │          │ 6.5+20250216-2              │               │ gnu-ncurses: ncurses Stack Buffer Overflow                   │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-6141                    │
├────────────────┤                     │          │          │                             ├───────────────┤                                                              │
│ ncurses-bin    │                     │          │          │                             │               │                                                              │
│                │                     │          │          │                             │               │                                                              │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ passwd         │ CVE-2007-5686       │          │          │ 1:4.17.4-2                  │               │ initscripts in rPath Linux 1 sets insecure permissions for   │
│                │                     │          │          │                             │               │ the /var/lo ......                                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2007-5686                    │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2024-56433      │          │          │                             │               │ shadow-utils: Default subordinate ID configuration in        │
│                │                     │          │          │                             │               │ /etc/login.defs could lead to compromise                     │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2024-56433                   │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ TEMP-0628843-DBAD28 │          │          │                             │               │ [more related to CVE-2005-4890]                              │
│                │                     │          │          │                             │               │ https://security-tracker.debian.org/tracker/TEMP-0628843-DB- │
│                │                     │          │          │                             │               │ AD28                                                         │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ perl-base      │ CVE-2011-4116       │          │          │ 5.40.1-6                    │               │ perl: File:: Temp insecure temporary file handling           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2011-4116                    │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ sysvinit-utils │ TEMP-0517018-A83CE6 │          │          │ 3.14-4                      │               │ [sysvinit: no-root option in expert installer exposes        │
│                │                     │          │          │                             │               │ locally exploitable security flaw]                           │
│                │                     │          │          │                             │               │ https://security-tracker.debian.org/tracker/TEMP-0517018-A8- │
│                │                     │          │          │                             │               │ 3CE6                                                         │
├────────────────┼─────────────────────┤          │          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ tar            │ CVE-2005-2541       │          │          │ 1.35+dfsg-3.1               │               │ tar: does not properly warn the user when extracting setuid  │
│                │                     │          │          │                             │               │ or setgid...                                                 │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2005-2541                    │
│                ├─────────────────────┤          │          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ TEMP-0290435-0B57B5 │          │          │                             │               │ [tar's rmt command may have undesired side effects]          │
│                │                     │          │          │                             │               │ https://security-tracker.debian.org/tracker/TEMP-0290435-0B- │
│                │                     │          │          │                             │               │ 57B5                                                         │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ util-linux     │ CVE-2025-14104      │ MEDIUM   │          │ 2.41-5                      │               │ util-linux: util-linux: Heap buffer overread in setpwnam()   │
│                │                     │          │          │                             │               │ when processing 256-byte usernames                           │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2025-14104                   │
│                ├─────────────────────┼──────────┤          │                             ├───────────────┼──────────────────────────────────────────────────────────────┤
│                │ CVE-2022-0563       │ LOW      │          │                             │               │ util-linux: partial disclosure of arbitrary files in chfn    │
│                │                     │          │          │                             │               │ and chsh when compiled...                                    │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2022-0563                    │
├────────────────┼─────────────────────┼──────────┤          ├─────────────────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ zlib1g         │ CVE-2026-27171      │ MEDIUM   │          │ 1:1.3.dfsg+really1.3.1-1+b1 │               │ zlib: zlib: Denial of Service via infinite loop in CRC32     │
│                │                     │          │          │                             │               │ combine functions...                                         │
│                │                     │          │          │                             │               │ https://avd.aquasec.com/nvd/cve-2026-27171                   │
└────────────────┴─────────────────────┴──────────┴──────────┴─────────────────────────────┴───────────────┴──────────────────────────────────────────────────────────────┘

Python (python-pkg)

Total: 6 (UNKNOWN: 0, LOW: 2, MEDIUM: 1, HIGH: 3, CRITICAL: 0)

┌───────────────────────────┬────────────────┬──────────┬────────┬───────────────────┬───────────────┬──────────────────────────────────────────────────────────────┐
│          Library          │ Vulnerability  │ Severity │ Status │ Installed Version │ Fixed Version │                            Title                             │
├───────────────────────────┼────────────────┼──────────┼────────┼───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ Flask (METADATA)          │ CVE-2026-27205 │ LOW      │ fixed  │ 3.0.3             │ 3.1.3         │ flask: Flask: Information disclosure via improper caching of │
│                           │                │          │        │                   │               │ session data                                                 │
│                           │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2026-27205                   │
├───────────────────────────┼────────────────┼──────────┤        ├───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ jaraco.context (METADATA) │ CVE-2026-23949 │ HIGH     │        │ 5.3.0             │ 6.1.0         │ jaraco.context: jaraco.context: Path traversal via malicious │
│                           │                │          │        │                   │               │ tar archives                                                 │
│                           │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2026-23949                   │
├───────────────────────────┼────────────────┼──────────┤        ├───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ pip (METADATA)            │ CVE-2025-8869  │ MEDIUM   │        │ 24.0              │ 25.3          │ pip: pip missing checks on symbolic link extraction          │
│                           │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2025-8869                    │
│                           ├────────────────┼──────────┤        │                   ├───────────────┼──────────────────────────────────────────────────────────────┤
│                           │ CVE-2026-1703  │ LOW      │        │                   │ 26.0          │ pip: pip: Information disclosure via path traversal when     │
│                           │                │          │        │                   │               │ installing crafted wheel archives...                         │
│                           │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2026-1703                    │
├───────────────────────────┼────────────────┼──────────┤        ├───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ wheel (METADATA)          │ CVE-2026-24049 │ HIGH     │        │ 0.45.1            │ 0.46.2        │ wheel: wheel: Privilege Escalation or Arbitrary Code         │
│                           │                │          │        │                   │               │ Execution via malicious wheel file...                        │
│                           │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2026-24049                   │
│                           │                │          │        │                   │               │                                                              │
│                           │                │          │        │                   │               │                                                              │
│                           │                │          │        │                   │               │                                                              │
│                           │                │          │        │                   │               │                                                              │
└───────────────────────────┴────────────────┴──────────┴────────┴───────────────────┴───────────────┴──────────────────────────────────────────────────────────────┘

```

A imagem de exemplo possui diversas vulnerabilidades reconhecidas, que são as CVE's (Common Vulnerabilities and Exposures). As CVE's podem ser consultadas no National Vulnerability Database https://nvd.nist.gov/

Agora realizando o teste com uma imagem distroless, podemos validar que há apenas uma vulnerabilidade:

```
$ admin@jupiter:~$ trivy image giropops-senha:3.0
2026-02-26T07:13:22Z	INFO	[vuln] Vulnerability scanning is enabled
2026-02-26T07:13:22Z	INFO	[secret] Secret scanning is enabled
2026-02-26T07:13:22Z	INFO	[secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2026-02-26T07:13:22Z	INFO	[secret] Please see https://trivy.dev/docs/v0.69/guide/scanner/secret#recommendation for faster secret detection
2026-02-26T07:13:22Z	INFO	Detected OS	family="wolfi" version="20230201"
2026-02-26T07:13:22Z	INFO	[wolfi] Detecting vulnerabilities...	pkg_num=75
2026-02-26T07:13:22Z	INFO	Number of language-specific files	num=1
2026-02-26T07:13:22Z	INFO	[python-pkg] Detecting vulnerabilities...
2026-02-26T07:13:22Z	INFO	Table result includes only package filenames. Use '--format json' option to get the full path to the package file.

Report Summary

┌──────────────────────────────────────────────────────────────────────────────────┬────────────┬─────────────────┬─────────┐
│                                      Target                                      │    Type    │ Vulnerabilities │ Secrets │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ giropops-senha:3.0 (wolfi 20230201)                                              │   wolfi    │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/blinker-1.9.0.dist-info/METADA- │ python-pkg │        0        │    -    │
│ TA                                                                               │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/click-8.3.1.dist-info/METADATA  │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/flask-3.0.3.dist-info/METADATA  │ python-pkg │        1        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/itsdangerous-2.2.0.dist-info/M- │ python-pkg │        0        │    -    │
│ ETADATA                                                                          │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/jinja2-3.1.6.dist-info/METADATA │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/markupsafe-3.0.3.dist-info/MET- │ python-pkg │        0        │    -    │
│ ADATA                                                                            │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/prometheus_client-0.16.0.dist-- │ python-pkg │        0        │    -    │
│ info/METADATA                                                                    │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/redis-4.5.4.dist-info/METADATA  │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/werkzeug-3.1.6.dist-info/METAD- │ python-pkg │        0        │    -    │
│ ATA                                                                              │            │                 │         │
└──────────────────────────────────────────────────────────────────────────────────┴────────────┴─────────────────┴─────────┘
Legend:
- '-': Not scanned
- '0': Clean (no security findings detected)


Python (python-pkg)

Total: 1 (UNKNOWN: 0, LOW: 1, MEDIUM: 0, HIGH: 0, CRITICAL: 0)

┌──────────────────┬────────────────┬──────────┬────────┬───────────────────┬───────────────┬──────────────────────────────────────────────────────────────┐
│     Library      │ Vulnerability  │ Severity │ Status │ Installed Version │ Fixed Version │                            Title                             │
├──────────────────┼────────────────┼──────────┼────────┼───────────────────┼───────────────┼──────────────────────────────────────────────────────────────┤
│ Flask (METADATA) │ CVE-2026-27205 │ LOW      │ fixed  │ 3.0.3             │ 3.1.3         │ flask: Flask: Information disclosure via improper caching of │
│                  │                │          │        │                   │               │ session data                                                 │
│                  │                │          │        │                   │               │ https://avd.aquasec.com/nvd/cve-2026-27205                   │
└──────────────────┴────────────────┴──────────┴────────┴───────────────────┴───────────────┴──────────────────────────────────────────────────────────────┘
```

Acima está descrito uma vulnerabilidade do Flask, onde é corrigido na versão 3.1.3. Então, se alterarmos a versão do flask e re-buildarmos a nossa imagem, não temos nenhuma:

```
$ admin@jupiter:~/giropops-senhas$ trivy image giropops-senha:4.0
2026-02-26T07:18:12Z	INFO	[vuln] Vulnerability scanning is enabled
2026-02-26T07:18:12Z	INFO	[secret] Secret scanning is enabled
2026-02-26T07:18:12Z	INFO	[secret] If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2026-02-26T07:18:12Z	INFO	[secret] Please see https://trivy.dev/docs/v0.69/guide/scanner/secret#recommendation for faster secret detection
2026-02-26T07:18:21Z	INFO	[python] Licenses acquired from one or more METADATA files may be subject to additional terms. Use `--debug` flag to see all affected packages.
2026-02-26T07:18:21Z	INFO	Detected OS	family="wolfi" version="20230201"
2026-02-26T07:18:21Z	INFO	[wolfi] Detecting vulnerabilities...	pkg_num=75
2026-02-26T07:18:21Z	INFO	Number of language-specific files	num=1
2026-02-26T07:18:21Z	INFO	[python-pkg] Detecting vulnerabilities...

Report Summary

┌──────────────────────────────────────────────────────────────────────────────────┬────────────┬─────────────────┬─────────┐
│                                      Target                                      │    Type    │ Vulnerabilities │ Secrets │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ giropops-senha:4.0 (wolfi 20230201)                                              │   wolfi    │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/blinker-1.9.0.dist-info/METADA- │ python-pkg │        0        │    -    │
│ TA                                                                               │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/click-8.3.1.dist-info/METADATA  │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/flask-3.1.3.dist-info/METADATA  │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/itsdangerous-2.2.0.dist-info/M- │ python-pkg │        0        │    -    │
│ ETADATA                                                                          │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/jinja2-3.1.6.dist-info/METADATA │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/markupsafe-3.0.3.dist-info/MET- │ python-pkg │        0        │    -    │
│ ADATA                                                                            │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/prometheus_client-0.16.0.dist-- │ python-pkg │        0        │    -    │
│ info/METADATA                                                                    │            │                 │         │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/redis-4.5.4.dist-info/METADATA  │ python-pkg │        0        │    -    │
├──────────────────────────────────────────────────────────────────────────────────┼────────────┼─────────────────┼─────────┤
│ home/nonroot/.local/lib/python3.14/site-packages/werkzeug-3.1.6.dist-info/METAD- │ python-pkg │        0        │    -    │
│ ATA                                                                              │            │                 │         │
└──────────────────────────────────────────────────────────────────────────────────┴────────────┴─────────────────┴─────────┘
Legend:
- '-': Not scanned
- '0': Clean (no security findings detected)
```

---

### Docker Scout

Um outra alternativa para scans de vulnerabilidades é o Docker Scout, plugin do próprio Docker. A diferença entre as demais ferramentas, é que ele traz as recomendações de quais imagens utilizar, baseado em informações do Dockerhub:

