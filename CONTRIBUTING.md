
# Contributing guidelines

Please take a moment to review this document in order to make the contribution process easy and effective for everyone involved.

The following is a set of guidelines for contributing to the ON-API project.
These are mostly guidelines, not rules. Use your best judgment.

Following these guidelines helps to communicate that you respect the time of the developers managing and developing this open source project. In return, they should reciprocate that respect in addressing your issue or assessing patches and features.

#### Table Of Contents

[Code of Conduct](#code-of-conduct)

[Contact Information](#contact-information)

[How Can I Contribute?](#how-can-i-contribute)
  * [Reporting Bugs](#reporting-bugs)
  * [Suggesting Enhancements](#suggesting-enhancements)
  * [Pull Requests](#pull-requests)

[Styleguides](#styleguides)

## Code of Conduct

This project and everyone participating in it is governed by the [contributor covenant](https://www.contributor-covenant.org/version/1/4/code-of-conduct). By participating, you are expected to uphold this code. Please report unacceptable behavior to [teemu.frosen@ownit.se](mailto:teemu.frosen@ownit.se).

## Contact Information

We use slack for communication and trello for planning.
Please get in touch with our maintainers and ask for direction or if you need any other help.
Contact [teemu.frosen@ownit.se](mailto:teemu.frosen@ownit.se) if you need an invite to our slack or trello. Let us know if your companys domain name is missing from Trello.

* [Trello](https://trello.com/b/rkVUQebh/open-networks-api-general)
* [Slack](https://oppnanatapi.slack.com)

## How Can I Contribute?

### Suggesting Enhancements
Feature requests are welcome. But take a moment to find out whether your idea fits with the scope and aims of the project. Please provide as much detail and context as possible. 

### Pull Requests
Good pull requests - patches, improvements, new features - are a fantastic help. They should remain focused in scope and avoid containing unrelated commits.

**Please ask first** before embarking on any significant pull request (e.g. implementing features, refactoring code), otherwise you risk spending a lot of time working on something that wont fit or align with the direction and scope of the project.

The process described here has several goals:

- Maintain ON-API's quality
- Fix problems that are important to users
- Engage the community in working toward the best possible specification 

Please follow these steps for your contribution:

1. Use the [template](2.4.0/common/specification_template.md) for new specifications
2. Make use of the already defined data formats, models and responses placed in the common [folder](2.4.0/common)
3. Follow the design [guidelines](#guidelines)
4. [Fork](http://help.github.com/fork-a-repo/) the repo, clone your fork,
   and configure the remotes:

   ```bash
   # Clone your fork of the repo into the current directory
   git clone https://github.com/<your-username>/on-api
   # Navigate to the newly cloned directory
   cd on-api
   # Assign the original repo to a remote called "upstream"
   git remote add upstream https://github.com/on-api/on-api
   ```

5. If you cloned a while ago, get the latest changes from upstream:

   ```bash
   git checkout master
   git pull upstream master
   ```

6. Create a new topic branch (off the main project development branch) to
   contain your feature, change, or fix:

   ```bash
   git checkout -b <topic-branch-name>
   ```

7. Commit your changes in logical chunks. Use Git's [interactive rebase](https://help.github.com/articles/interactive-rebase) feature to tidy up your commits before making them public.

8. Consider updating the changelog

10. Locally merge (or rebase) the upstream master branch into your topic branch:

   ```bash
   git pull [--rebase] upstream master
   ```

11. Push your topic branch up to your fork:

   ```bash
   git push origin <topic-branch-name>
   ```

12. [Open a Pull Request](https://help.github.com/articles/using-pull-requests/) with a clear title and description.

The reviewer(s) may ask you to complete additional design work, tests, or other changes before your pull request can be ultimately accepted. Please note that we follow humble release cycles.

## Styleguides

- Use [Markdown](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)
- Follow the REST architecture style when describing HTTP endpoints
- Make use of [HTTP status codes](2.4.0/common/respones.md)
- Use HTTP headers to filter data. eg. `If-Modified-Since`.
- Or query params, eg. `GET /resouce?key=val`
- Reuse [data formats](#common/dataformats.md)
- git commit message [guidelines](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
