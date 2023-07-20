# What is Packaging System?

*Major Packaging System Families*
|Packaging System|Distributions(Partial Listing)|
|---|---|
|Debian Style(.deb)|Debian, Ubuntu, Linux Mint, Raspbian|
|Red Hat Style(.rpm)|Fdeora, CentOS, Red Hat Linux, OpenSUSE|

*Packaging System Tools*
- Low-level tools which handle tasks such as installing and removing package files
- High-level tools that perform metadata searching and dependency resolution

|Distributions|Low-Level Tools|High-Level Tools|
|---|---|---|
|Debian Style|dpkg|apt, apt-get, aptitude|
|Red Hat Style|rpm|yum, dnf|

# apt reporitory
**Ref**: https://askubuntu.com/questions/343333/whats-the-difference-between-a-ppa-and-a-repository

Personal Package Archives (PPA) allow you to upload Ubuntu source packages to be built and published as an apt repository by Launchpad.

- A repository is a collection of packages, hosted on an arbitrary server.
- A PPA is also a collection of packages, hosted on the Launchpad servers.
- Thus, a PPA is a special kind of repository. Like a square is a special kind of rectangle.