source "https://rubygems.org"

gem 'puppet', '3.3.2'

def location_for(place, fake_version = nil)
  if place =~ /^(git:[^#]*)#(.*)/
    [fake_version, { :git => $1, :branch => $2, :require => false }].compact
  elsif place =~ /^file:\/\/(.*)/
    ['>= 0', { :path => File.expand_path($1), :require => false }]
  else
    [place, { :require => false }]
  end
end

# C Ruby (MRI) or Rubinius, but NOT Windows
platforms :ruby do
  gem 'pry', :group => :development
  gem 'yard', :group => :development
  gem 'redcarpet', '~> 2.0', :group => :development
  gem "racc", "1.4.9", :group => :development
end

#gem "puppet", :path => File.dirname(__FILE__), :require => false
gem "facter", *location_for(ENV['FACTER_LOCATION'] || '~> 1.6')
gem "hiera", *location_for(ENV['HIERA_LOCATION'] || '~> 1.0')
gem "rake", :require => false
gem "rgen", "0.6.5", :require => false


group(:development, :test) do

  # Jenkins workers may be using RSpec 2.9, so RSpec 2.11 syntax
  # (like `expect(value).to eq matcher`) should be avoided.
  gem "rspec", "~> 2.11.0", :require => false
  gem "rspec-puppet"
  # Mocha is not compatible across minor version changes; because of this only
  # versions matching ~> 0.10.5 are supported. All other versions are unsupported
  # and can be expected to fail.
  gem "mocha", "~> 0.10.5", :require => false
  gem 'json_pure', '2.0.1' # pin this puppet dependency to 1.9-compat version
  gem "yarjuf", "~> 1.0"
end

group(:extra) do
  gem "rack", "~> 1.4", :require => false
  gem "activerecord", '~> 3.0.7', :require => false
  gem "couchrest", '~> 1.0', :require => false
  gem "net-ssh", '~> 2.1', :require => false
  gem "puppetlabs_spec_helper", :require => false
  gem "sqlite3", :require => false
  gem "stomp", :require => false
  gem "tzinfo", :require => false
end

platforms :mswin, :mingw do
  gem "ffi", "1.9.0", :require => false
  gem "sys-admin", "1.5.6", :require => false
  gem "win32-api", "1.4.8", :require => false
  gem "win32-dir", "0.4.3", :require => false
  gem "win32-eventlog", "0.5.3", :require => false
  gem "win32-process", "0.6.5", :require => false
  gem "win32-security", "0.1.4", :require => false
  gem "win32-service", "0.7.2", :require => false
  gem "win32-taskscheduler", "0.2.2", :require => false
  gem "win32console", "1.3.2", :require => false
  gem "windows-api", "0.4.2", :require => false
  gem "windows-pr", "1.2.2", :require => false
  gem "minitar", "0.5.4", :require => false
end

if File.exists? "#{__FILE__}.local"
  eval(File.read("#{__FILE__}.local"), binding)
end

# vim:filetype=ruby
