# Why this fork?
Just in case I don't get to update this and/or forget: https://github.com/unboxed/rspec-sitemap-matchers/pull/3

# RSpec sitemap matchers

Sitemap [protocol](http://www.sitemaps.org/protocol.html) matchers for RSpec.

Sitemaps are an easy way to inform search engines about pages on their sites that are available for crawling. In its simplest form, a Sitemap is an XML file that lists URLs for a site along with additional metadata about each URL (when it was last updated, how often it usually changes, and how important it is, relative to other URLs in the site) so that search engines can more intelligently crawl the site.

## Installation

Add this line to your application's Gemfile:

    gem 'rspec-sitemap-matchers'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rspec-sitemap-matchers

These matchers are not loaded by default in order not to pollute the global RSpec matcher namespace and consequentially to be able to specify in which context you would want to make use of them.

You can load them globally via your `spec_helper` (not recommended):

    RSpec.configure do |config|
      config.include RSpec::Sitemap::Matchers
    end

… or `include RSpec::Sitemap::Matchers` in an individual spec file (preferred way).

## Usage

These matchers can be used on `File`s, `String`s and any arbitary `IO` instance that has a `:read` method:

    describe "My Sitemap" do
    
      subject { File.open(Rails.root + 'tmp' + 'sitemap.xml') }

      it { should include_url("http://www.example.com") }
      it { should_not include_url("http://www.a-different-example.com") }

    end

The matchers also support more specific attribution matching, such as priorities as per the Sitemap protocol. These can be chained together:

    it { should include_url('http://www.example.com').priority(0.5) }
    it { should include_url('http://www.example.com').changefreq('weekly') }
    it { should include_url('http://www.example.com').lastmod('2012-07-16T19:20+01:00') }

Note: You can chanin multiple attribute matchers together, like `.lastod('…').changefreq('…')` etc.

## Planned features

* Stricter markup and structure validation
* Encoding validation matcher (Sitemaps must be UTF-8 encoded)
* `be_a_valid_sitemap` matcher

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Write meaningful and readable tests
4. Make the tests pass (ie implement your changes)
5. Commit your changes (`git commit -am 'Add some feature'`)
6. Push to the branch (`git push origin my-new-feature`)
7. Create new Pull Request

## Copyright

Copyright © 2012 Attila Györffy, [Unboxed Consulting](http://www.unboxedconsulting.com) and [contributors](http://github.com/unboxed/rspec-sitemap-matchers/graphs/contributors). See LICENSE for details.
