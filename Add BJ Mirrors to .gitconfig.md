####  Add BJ Mirrors to .gitconfig



`~/.gitconfig`

```bash
  1 # This is Git's per-user configuration file.
  2 [user]
  3 # Please adapt and uncomment the following lines:
  4     name = zhhp1001
  5     email = zhhp@tju.edu.cn
  6 [url "ssh://icggerrit.bj.intel.com:29418/"]
  7     insteadOf = ssh://icggerrit.corp.intel.com:29418/
  8     insteadOf = ssh://icggerrit:29418/
  9 [url "ssh://icggerrit.corp.intel.com:29418/"]
 10     pushInsteadOf = ssh://icggerrit.corp.intel.com:29418/
 11     pushInsteadOf = ssh://icggerrit:29418/
 12     pushInsteadOf = ssh://icggerrit.bj.intel.com:29418/
 13 [url "ssh://hzhen@icggerrit.bj.intel.com:29418/"]
 14     insteadOf = ssh://hzhen@icggerrit.corp.intel.com:29418/
 15 [url "ssh://hzhen@icggerrit.corp.intel.com:29418/"]
 16     pushInsteadOf = ssh://hzhen@icggerrit.corp.intel.com:29418/
 17     pushInsteadOf = ssh://hzhen@icggerrit.bj.intel.com:29418/
 18 [url "https://icggerrit.bj.intel.com/"]
 19     insteadOf = https://icggerrit.corp.intel.com/
 20 [url "https://icggerrit.corp.intel.com/"]
 21     pushInsteadOf = https://icggerrit.corp.intel.com/
 22 [url "https://hzhen@icggerrit.bj.intel.com/"]
 23     insteadOf = https://hzhen@icggerrit.corp.intel.com/
 24 [url "https://hzhen@icggerrit.corp.intel.com/"]
 25     pushInsteadOf = https://hzhen@icggerrit.corp.intel.com/
 26 [review "ssh://icggerrit.corp.intel.com"]
 27 username = hzhen
 28 [review "https://icggerrit.corp.intel.com"]
 29 username = hzhen
 30 [review "https://android.intel.com"]
 31 username = hzhen
 32 [color]
 33     ui = auto
 34 [filter "lfs"]
 35     process = git-lfs filter-process
 36     required = true
 37     clean = git-lfs clean -- %f
 38     smudge = git-lfs smudge -- %f

```

Line26 to 31 is important. 