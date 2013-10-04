# Project Checklist

## Overall

### Create a Gemfile

`touch Gemfile`

Add the following line to your Gemfile

`source 'https://rubygems.org'`

After adding *any* gem to your Gemfile, you must run `bundle install`. 

### Create a .gitignore

`touch .gitignore`

Add any files that you wouldn't want in your git repo. Below is a common set:

```
*.gem
*.rbc
.bundle
.config
coverage
InstalledFiles
lib/bundler/man
pkg
rdoc
spec/reports
test/tmp
test/version_tmp
tmp
.DS_Store
.yardoc
_yardoc
doc/
```

### Initalize a Git repo

`git init`

### Create or fork repo on Github

On Github, create or fork a repo. Add this repo as your origin.

`git remote add origin git@github.com:USER-NAME/REPO-NAME.git`

### Create a lib directory to hold code

`mkdir lib`

## [RSpec](https://github.com/rspec/rspec)

Add Rspec to your Gemfile

`gem 'rspec'`

Run 

`rspec --init` to create your `.rspec` and `spec/spec_helper.rb` files.

Create a `spec/FOO_spec.rb` file with `touch spec/FOO_spec.rb` and start it with the following lines:

```
require 'spec_helper'
require_relative '../lib/FOO.rb'

describe Foo do
end
```

Run the tests by running `rspec spec` from your project's root directory.

Write tests first, then code. Use [PairProgrammingBot](http://pairprogrammingbot.com/) if you can't remember the TDD cycle. 

## [travis](http://about.travis-ci.org/docs/user/languages/ruby/)

Create a `.travis.yml` file.

`touch .travis.yml`

Put the following code in your `.travis.yml`

```
language: ruby
rvm:
  - "2.0.0"
script: "bundle exec rspec spec"
```

Go to [Travis CI](https://travis-ci.org/) and once you've pushed your repo to Github, enable the repo in your "Accounts" settings. It takes a few minutes for the tests to run and new repos to appear. 

## [simplecov](https://github.com/colszowka/simplecov)

Add Simplecov to your Gemfile

`gem 'simplecov', require: false`

Once we're using Rails, we'll put in the following instead:

`gem 'simplecov', require: false, group: :test`

At the top of you `spec/spec_helper.rb` add the following code before anything else: 

```
require 'json'
require 'simplecov'
SimpleCov.start
```

Ensure that you have the `coverage` directory added to your `.gitignore` file. When you run your spec tests, coverage reports will be generated to `coverage/index.html` which you can open in a browser by typing `open coverage/index.html`

## [pry](https://github.com/pry/pry)

Add Pry to your Gemfile

`gem 'pry'`

Run `pry` from the bash prompt. 

Insert `binding.pry` at any point in your code to halt execution when that is reached. Exit pry by typing `quit` and completely stop the program with `exit-program`. 

## [guard](https://github.com/guard/guard)

Add Guard to your Gemfile

`gem 'guard'`

Create a Guardfile with `touch Guardfile` and add the following to it: 

```
guard :rspec do
  watch(%r{^spec/.+_spec\.rb$})
  watch(%r{^lib/(.+)\.rb$})    { |m| "spec/#{m[1]}_spec.rb" }
  watch('spec/spec_helper.rb')  { "spec" }
end
```

Run `bundle exec guard --clear` 


