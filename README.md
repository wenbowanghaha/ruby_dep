# RubyDep

[![Gem Version](https://img.shields.io/gem/v/no_deps.svg?style=flat)](https://rubygems.org/gems/no_deps) [![Build Status](https://travis-ci.org/e2/no_deps.svg)](https://travis-ci.org/e2/no_deps)

## The problem

Your gem doesn't support all possible Ruby versions.

So, you need to tell users which Ruby versions you support in:

1. Your gemspec
2. Your README
3. Your .travis.yml file

That breaks the principle of single responsibility.


## The solution

This gems detects which versions of Ruby your project supports.

It assumes you are using Travis and the versions listed in your `.travis.yml` are supported.

This helps you limit the Ruby versions you support - just by adding/removing entries in your Travis configuration file.



## Usage

E.g. in your gemspec file:

```ruby
  begin
    require "ruby_dep/travis"
    s.required_ruby_version = RubyDep::Travis.new.version_constraint
  rescue LoadError
    abort "Install 'ruby_dep' gem before building this gem"
  end

  s.add_development_dependency 'ruby_dep', '~> 1.0'
```

In your `README.md`:

Replace your mentions of "supported Ruby versions" to point to the Travis build.

(Or, you can point to the rubygems.org site where the required Ruby version is listed).

If it works on Travis, it's assumed to be supported, right? 

If it fails, it isn't, right?

## Roadmap

Pull Requests are welcome.

Plans include: reading supported Ruby from `.rubocop.yml` (`TargetRubyVersion` field).


## Development

Use `rake` to run tests.

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/e2/ruby_dep.

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
