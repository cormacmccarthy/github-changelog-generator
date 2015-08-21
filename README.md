[![Gem Version](https://badge.fury.io/rb/github_changelog_generator.svg)](http://badge.fury.io/rb/github_changelog_generator)
[![Dependency Status](https://gemnasium.com/skywinder/github-changelog-generator.svg)](https://gemnasium.com/skywinder/github-changelog-generator)
[![Build Status](https://travis-ci.org/skywinder/github-changelog-generator.svg?branch=master)](https://travis-ci.org/skywinder/github-changelog-generator)
[![Inline docs](http://inch-ci.org/github/skywinder/github-changelog-generator.svg)](http://inch-ci.org/github/skywinder/github-changelog-generator)
[![Code Climate](https://codeclimate.com/github/skywinder/github-changelog-generator/badges/gpa.svg)](https://codeclimate.com/github/skywinder/github-changelog-generator)
[![Test Coverage](https://codeclimate.com/github/skywinder/github-changelog-generator/badges/coverage.svg)](https://codeclimate.com/github/skywinder/github-changelog-generator)

GitHub Changelog Generator ![GitHub Logo](../master/images/logo.jpg)
==================

  - [Installation](#installation)
  - [Output example](#output-example)
  - [Usage](#usage)
    - [Params](#params)
    - [GitHub token](#github-token)
  - [Features and advantages of this project](#features-and-advantages-of-this-project)
    - [Alternatives](#alternatives)
    - [Projects using this library](#projects-using-this-library)
  - [Am I missing some essential feature?](#am-i-missing-some-essential-feature)
  - [Contributing](#contributing)
  - [License](#license)

 
### Changelog generation has never been so easy:

**Fully automate changelog generation** - This gem generates change log file based on **tags**, **issues** and merged **pull requests** (and splits them into separate lists according labels) from :octocat: GitHub Issue Tracker.

Since now you don't have to fill your `CHANGELOG.md` manually: just run the script, relax and take a cup of :coffee: before your next release! :tada:

>### *What’s the point of a change log?*
To make it easier for users and contributors to see precisely what notable changes have been made between each release (or version) of the project.
### *Why should I care?*
Because software tools are for people. If you don’t care, why are you contributing to open source? Surely, there must be a kernel (ha!) of care somewhere in that lovely little brain of yours.

> :copyright: *[http://keepachangelog.com](http://keepachangelog.com/)*

## Installation

	[sudo] gem install github_changelog_generator

## Output example

- Look at **[CHANGELOG.md](https://github.com/skywinder/Github-Changelog-Generator/blob/master/CHANGELOG.md)** for this project
- [ActionSheetPicker-3.0/CHANGELOG.md](https://github.com/skywinder/ActionSheetPicker-3.0/blob/master/CHANGELOG.md)  was generated by command:

		github_changelog_generator -u skywinder -p ActionSheetPicker-3.0

- In general it looks like this:

> ## [1.2.5](https://github.com/skywinder/Github-Changelog-Generator/tree/1.2.5) (2015-01-15)
> 
> [Full Changelog](https://github.com/skywinder/Github-Changelog-Generator/compare/1.2.4...1.2.5)
> 
> **Implemented enhancements:**
> 
> - Use milestone to specify in which version bug was fixed [\#22](https://github.com/skywinder/Github-Changelog-Generator/issues/22)
> 
> **Fixed bugs:**
> 
> - Error when trying to generate log for repo without tags [\#32](https://github.com/skywinder/Github-Changelog-Generator/issues/32)
> 
> **Merged pull requests:**
> 
> - PrettyPrint class is included using lowercase 'pp' [\#43](https://github.com/skywinder/Github-Changelog-Generator/pull/43) ([schwing](https://github.com/schwing))
> 
> - support enterprise github via command line options [\#42](https://github.com/skywinder/Github-Changelog-Generator/pull/42) ([glenlovett](https://github.com/glenlovett))


## Usage
**It's really simple**: 

- If your **git remote** `origin` refers to your GitHub repo, then just go to your project folder and run:

		github_changelog_generator

-  or from anywhere:
    - `github_changelog_generator -u github_username -p github_project`
    - `github_changelog_generator  github_username/github_project`
     
As output you will get `CHANGELOG.md` file with pretty *Markdown-formatted* changelog.

### Params
Type `github_changelog_generator --help` for details.

More detailed info about params you can find in Wiki page: [**Advanced change log generation examples**](https://github.com/skywinder/github-changelog-generator/wiki/Advanced-change-log-generation-examples)

### GitHub token

Since GitHub allows you to make only 50 requests without authentication it's recommended to run this script with a token (`-t, --token` option)

**You can easily [generate it here](https://github.com/settings/tokens/new?description=GitHub%20Changelog%20Generator%20token)**.

And:

- Run with key `-t [your-40-digit-token]` 
- Or set environment variable `CHANGELOG_GITHUB_TOKEN` and specify there your token. 
 		
	i.e. add to your `~/.bash_profile` or `~/.zshrc` or any other place to load ENV variables string :

        export CHANGELOG_GITHUB_TOKEN="your-40-digit-github-token"

So, if you got error like this:
>! /Library/Ruby/Gems/2.0.0/gems/github_api-0.12.2/lib/github_api/response/raise_error.rb:14:in `on_complete'

It's time to create this token or wait for 1 hour before GitHub reset the counter for your IP.


### Rake task

You love Rake? So do we! And so we've made it easier for you by providing a Rake task library for your Change log generation. In your Rakefile, use:

```ruby
GitHubChangelogGenerator::RakeTask.new :changelog do |config|
  config.since_tag = '0.1.14'
  config.future_release = '0.2.0'
end
```

All command line options can be passed to the Rake task as `config` parameters. Since you're naming the Rake task yourself, you can create as many as you want, too.

##Features and advantages of this project
- Generate canonical, neat change log file, followed by [basic change log guidelines](http://keepachangelog.com/) :gem:
- Possible to generate **Unreleased** changes (closed issues that have not released yet) :dizzy:
- **GitHub Enterprise support** via command line options! :factory:
- Flexible format **customisation**:
    - **Customize** issues, that **should be added** to changelog :eight_spoked_asterisk:
    - **Custom date format** supported (but get in mind [ISO 8601](http://xkcd.com/1179/) ) :date:
    - Ability to manually specify in which version issue was fixed (in case, when closed date is not match) by setting `milestone` of issue the same name as tag of  required version :pushpin:
    - Automatically **exclude specific issues**, not-related to change log (any issue, that has label `question` `duplicate` `invalid` `wontfix`by default)  :scissors:
- **Distinguish** issues **according labels**. :mag_right:
    - Merged pull requests (all `merged` pull-requests) :twisted_rightwards_arrows:
    - Bug fixes (by label `bug` in issue) :beetle:
    - Enhancements (by label `enhancement` in issue) :star2:
    - 	Issues (closed issues `w/o any labels`) :non-potable_water:    

- You can manually set which labels should be included/excluded. :wrench:
- Apply a lot of other customisations, to fit changelog for your personal style :tophat: 
(*look `github_changelog_generator --help`  for details)*


###Alternatives
Here is a [wikipage list of alternatives](https://github.com/skywinder/Github-Changelog-Generator/wiki/Alternatives), that I found. But none satisfied my requirements.

*If you know other projects - feel free to edit this Wiki page!*


### Projects using this library
[Wikipage with list of projects](https://github.com/skywinder/Github-Changelog-Generator/wiki/Projects-using-Github-Changelog-Generator) 

If you've used this project in a live app, please let me know! Nothing makes me happier than seeing someone else take my work and go wild with it.

*If you are using `github_changelog_generator` for generation change log in your project or know another project that uses it, please add it to [this] (https://github.com/skywinder/Github-Changelog-Generator/wiki/Projects-using-Github-Changelog-Generator) list.*

## Am I missing some essential feature?

- **Nothing is impossible!** 

- Open an [issue](https://github.com/skywinder/Github-Changelog-Generator/issues/new) and let's make generator better together! 

- *Bug reports, feature requests, patches, well-wishes are always welcome* :heavy_exclamation_mark:

## FAQ

- ***I already use GitHub Releases. Why do I need this?***

GitHub Releases is a very good thing. And it's very good practice to maintain it (not so much people using it yet)! :congratulations:

*BDW: I would like to support GitHub Releases in [next releases](https://github.com/skywinder/github-changelog-generator/issues/56) ;)*

I'm not try to compare quality of auto-generated and manually generated logs.. but:

The auto generated Changelog really helps even if you manually fill Releases notes!

For example:

When I found a closed bug - it's very useful to understand, in which release it was fixed. In that case you can easily find this issue by \# in `CHANGELOG.md`.

- it's not so quite easy to find it in manually filled Releases notes.
- this file can also help you to build your Release note and not miss features in manually-filled list.

In the end:

I think, that GitHub Releases is more for end-users.
But `CHANGELOG.md` could stay in the repo for developers with detailed list of changes.
And it's nothing bad to combine GitHub Releases and `CHANGELOG.md` file together in that manner.

- ***I received a warning: GitHub API rate limit exceed, what does this mean?***

GitHub [limits the number of API requests](https://developer.github.com/v3/#rate-limiting) you can make in an hour. You can make up to 5,000 requests per hour. For unauthenticated requests, the rate limit allows you to make up to 60 requests per hour. Unauthenticated requests are associated with your IP address, and not the user making requests.

If you're seeing this warning:

1. Make sure you're providing an OAuth token so you're not anonymously making requests. This will increase the number of requests from 60 to 5000 per hour.
2. You probably have a large repo with lots of issues/PRs. You can use the `--max-issues NUM` argument to limit the number of issues that are pulled back. For example: `--max-issues 1000`

## Contributing

1. Create an issue to discuss about your idea
2. [Fork it] (https://github.com/skywinder/Github-Changelog-Generator/fork)
3. Create your feature branch (`git checkout -b my-new-feature`)
4. Commit your changes (`git commit -am 'Add some feature'`)
5. Push to the branch (`git push origin my-new-feature`)
6. Create a new Pull Request
7. Profit! :white_check_mark:

## License

Github Changelog Generator is released under the [MIT License](http://www.opensource.org/licenses/MIT).
