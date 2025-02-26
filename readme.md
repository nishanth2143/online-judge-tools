# Online Judge Tools

[![Travis](https://img.shields.io/travis/kmyk/online-judge-tools/master.svg)](https://travis-ci.org/kmyk/online-judge-tools)
[![AppVeyor](https://ci.appveyor.com/api/projects/status/f0jfg16ap6g91l40/branch/master?svg=true)](https://ci.appveyor.com/project/kmyk/online-judge-tools)
[![Documentation Status](https://readthedocs.org/projects/online-judge-tools/badge/?version=master)](https://online-judge-tools.readthedocs.io/en/master/)
[![PyPI](https://img.shields.io/pypi/pyversions/online-judge-tools.svg)](#)
[![PyPI](https://img.shields.io/pypi/status/online-judge-tools.svg)](#)
[![PyPI](https://img.shields.io/pypi/v/online-judge-tools.svg)](https://pypi.python.org/pypi/online-judge-tools)
[![PyPI](https://img.shields.io/pypi/l/online-judge-tools.svg)](#)
[![Downloads](https://pepy.tech/badge/online-judge-tools)](https://pepy.tech/project/online-judge-tools)
[![Join the chat at https://gitter.im/online-judge-tools/community](https://badges.gitter.im/online-judge-tools/community.svg)](https://gitter.im/online-judge-tools/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Tools for online judge services. Downloading sample cases, Testing/Submitting your code, and various utilities.

## Screencast

![screencast](https://user-images.githubusercontent.com/2203128/34708715-568b13c0-f557-11e7-97ef-9f6b646e4776.gif)

## Features

-   Download sample cases
    -   AtCoder
    -   yukicoder
    -   Anarchy Golf
    -   Codeforces
    -   HackerRank
    -   Aizu Online Judge (including the Arena)
    -   CS Academy
    -   PKU JudgeOnline
    -   Kattis
    -   Toph (Problem Archive)
    -   Facebook Hacker Cup
    -   Library Checker (<https://judge.yosupo.jp>)
-   Download system test cases
    -   yukicoder
    -   Aizu Online Judge
-   Login (with CUI and/or GUI)
    -   AtCoder
    -   yukicoder
    -   Codeforces
    -   HackerRank
    -   Topcoder
    -   Toph
-   Submit your solution
    -   AtCoder
    -   yukicoder
    -   Codeforces
    -   HackerRank
    -   Topcoder (Marathon Match)
    -   Toph (Problem Archive)
-   ~~Generate scanner for input~~  (removed, use [kyuridenamida/atcoder-tools](https://github.com/kyuridenamida/atcoder-tools))
    -   AtCoder
    -   yukicoder
-   Test your solution
-   Test your solution for reactive problem
-   Generate input files from generators
-   Generate output files from input and reference implementation
-   Split an input file with many cases to files

## How to install

### using compiled binary

The portable executables `oj.exe` for Windows are downloadable from [GitHub releases](https://github.com/kmyk/online-judge-tools/releases).

### from PyPI

The package is <https://pypi.python.org/pypi/online-judge-tools>.

``` sh
$ pip3 install online-judge-tools
```

It requires Python 3.5 or later.

### from this repository

``` sh
$ git clone https://github.com/kmyk/online-judge-tools
$ cd online-judge-tools
$ pip3 install -e .
```

## How to use

``` sh
$ oj [download,login] URL
$ oj submit URL FILE [-l LANGUAGE]
$ oj test [-c COMMAND] [TEST...]
```

For details, see `--help`.

## Example

``` sh
$ oj download http://agc001.contest.atcoder.jp/tasks/agc001_a
[+] problem recognized: <onlinejudge.atcoder.AtCoder object at 0x7f2925a5df60>
[x] GET: http://agc001.contest.atcoder.jp/tasks/agc001_a
[+] 200 OK

[*] sample 0
[x] input: 入力例 1
2
1 3 1 2
[+] saved to: test/sample-1.in
[x] output: 出力例 1
3
[+] saved to: test/sample-1.out

[*] sample 1
[x] input: 入力例 2
5
100 1 2 3 14 15 58 58 58 29
[+] saved to: test/sample-2.in
[x] output: 出力例 2
135
[+] saved to: test/sample-2.out

[*] sample 2
[x] input: Sample Input 1
2
1 3 1 2
[+] saved to: test/sample-3.in
[x] output: Sample Output 1
3
[+] saved to: test/sample-3.out

[*] sample 3
[x] input: Sample Input 2
5
100 1 2 3 14 15 58 58 58 29
[+] saved to: test/sample-4.in
[x] output: Sample Output 2
135
[+] saved to: test/sample-4.out
```

## How to use as a library

Read the documents: <https://online-judge-tools.readthedocs.io/en/master/>

## Example to use as a library

The next code lists the shortest submissions for problems of AtCoder Beginner Contest XXX.

``` python
#!/usr/bin/env python3
from onlinejudge.service.atcoder import *
for contest in AtCoderService().iterate_contests():
    if not contest.contest_id.startswith('abc'):
        for problem in contest.list_problems():
            submission = next(problem.iterate_submissions_where(status='AC', order='source_length'))
            problem_full_name = '{}: {} - {}'.format(contest.get_name(), problem.get_alphabet(), problem.get_name())
            shortest_info = '({} byte, {})'.format(submission.get_code_size(), submission.get_language_name())
            print(problem_full_name.ljust(60), submission.get_user_id().ljust(12), shortest_info)
```

Example output:

```
AtCoder Beginner Contest 121: A - White Cells                kotatsugame  (26 byte, Perl6 (rakudo-star 2016.01))
AtCoder Beginner Contest 121: B - Can you solve this?        kotatsugame  (49 byte, Octave (4.0.2))
AtCoder Beginner Contest 121: C - Energy Drink Collector     x20          (54 byte, Perl (v5.18.2))
AtCoder Beginner Contest 121: D - XOR World                  climpet      (40 byte, Perl (v5.18.2))
AtCoder Beginner Contest 120: A - Favorite Sound             kotatsugame  (25 byte, Awk (mawk 1.3.3))
AtCoder Beginner Contest 120: B - K-th Common Divisor        n4o847       (35 byte, Awk (mawk 1.3.3))
AtCoder Beginner Contest 120: C - Unification                kotatsugame  (32 byte, Octave (4.0.2))
AtCoder Beginner Contest 120: D - Decayed Bridges            x20          (154 byte, Perl (v5.18.2))
AtCoder Beginner Contest 119: A - Still TBD                  morio__      (22 byte, Sed (GNU sed 4.2.2))
AtCoder Beginner Contest 119: B - Digital Gifts              n4o847       (31 byte, Perl (v5.18.2))
AtCoder Beginner Contest 119: C - Synthetic Kadomatsu        kotatsugame  (135 byte, Perl (v5.18.2))
AtCoder Beginner Contest 119: D - Lazy Faith                 kotatsugame  (179 byte, Octave (4.0.2))
AtCoder Beginner Contest 118: A - B +/- A                    n4o847       (19 byte, Awk (mawk 1.3.3))
AtCoder Beginner Contest 118: B - Foods Loved by Everyone    kotatsugame  (37 byte, Perl6 (rakudo-star 2016.01))
...
```

## FAQ

-   I cannot install this tool. How should I do?
    -   Check versions of your Python. Also consider the use of Windows Subsystem for Linux (WSL) if you use Windows environment.
-   Are there features to manage templates or snippets?
    -   No. They are not the responsibility of this tool. You should use plugins of your editor, like [thinca/vim-template](https://github.com/thinca/vim-template) or [Shougo/deoplete.nvim](https://github.com/Shougo/deoplete.nvim).
-   I usually make one directory per one contest (or, site). Is there a support for this style?
    -   Yes. You can use `--directory` (`-d`) option. However, I recommend to make one directory per one problem.
-   Can I specify problems by their IDs or names, instead of URLs?
    -   No. I have tried it once, but it is actually not so convenient and only increases the maintenance cost.
-   I don't want to give my password to this program.
    -   This program stores only your session tokens. Use `oj login --use-brower=always ...` and read [onlinejudge/_implementation/command/login.py](https://github.com/kmyk/online-judge-tools/blob/master/onlinejudge/_implementation/command/login.py).

For other questions, use [Gitter](https://gitter.im/online-judge-tools/community) or other SNSs.

## Related Tools

conflicted:

-   [nodchip/OnlineJudgeHelper](https://github.com/nodchip/OnlineJudgeHelper)
-   [kyuridenamida/atcoder-tools](https://github.com/kyuridenamida/atcoder-tools)

not conflicted:

-   [shivawu/topcoder-greed](https://github.com/shivawu/topcoder-greed) for Topcoder Single Round Match
-   [FakePsyho/mmstats](https://github.com/FakePsyho/mmstats) for Topcoder Marathon Match
-   <https://community.topcoder.com/tc?module=Static&d1=applet&d2=plugins>

projects depending on kmyk/online-judge-tools:

1.  wrappers:
    -   [kjnh10/pcm](https://github.com/kjnh10/pcm)
    -   [Tatamo/atcoder-cli](https://github.com/Tatamo/atcoder-cli)
    -   one of my friends uses `oj` via shortcut keys of VSCode
1.  libraries using this for CI:
    -   [blue-jam/ProconLibrary](https://github.com/blue-jam/ProconLibrary) uses `oj` for CI
    -   [kmyk/competitive-programming-library](https://github.com/kmyk/competitive-programming-library) uses `oj` for CI
1.  others:
    -   [fukatani/rujaion](https://github.com/fukatani/rujaion) is an IDE for competitive-programming with Rust
    -   [kmyk/AtCoderProblemsStatic](https://github.com/kmyk/AtCoderProblemsStatic) is a clone of [kenkoooo/AtCoderProblems](https://github.com/kenkoooo/AtCoderProblems)
    -   [kmyk/atcoder-auto-debugger](https://github.com/kmyk/atcoder-auto-debugger) is a program to analyze submissions for AtCoder and find bugs

## Authors

-   owner: [@kmyk](https://github.com/kmyk) (AtCoder: [kimiyuki](https://atcoder.jp/users/kimiyuki), Codeforces: [kimiyuki](https://codeforces.com/profile/kimiyuki))
-   collaborator: [@fukatani](https://github.com/fukatani) (AtCoder: [ryoryoryo111](https://atcoder.jp/users/ryoryoryo111))

Also, patches are used sent from
[@kjnh10](https://github.com/kjnh10),
[@hachi-88](https://github.com/hachi-88),
[@Pachicobue](https://github.com/Pachicobue),
[@kfaRabi](https://github.com/kfaRabi),
[@tMasaaa](https://github.com/tMasaaa),
[@hamayanhamayan](https://github.com/hamayanhamayan),
[@yoshrc](https://github.com/yoshrc),
and [@kawacchu](https://github.com/kawacchu).

## License

MIT License
