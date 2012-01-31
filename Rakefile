require 'rake'
require 'bundler'
Bundler::GemHelper.install_tasks

require 'rspec/core/rake_task'

desc "Run specs"
RSpec::Core::RakeTask.new do |t|

end

desc "CI"
task :jetty do 
  require 'rails'
  require 'rails/generators'
  require 'blacklight/engine'
  require 'combustion'
  Combustion.initialize!
  load File.join(Blacklight.root,'lib','railties','solr_marc.rake')

  cwd = File.expand_path(Dir.pwd)

  Dir.chdir('spec/internal') do
    ENV['RAILS_ENV'] = "test" 
    ENV['CONFIG_PATH'] = File.join(Blacklight.root, "lib", "generators", "blacklight", "templates", "config", "SolrMarc", "config.properties")
    Rails::Generators.invoke("blacklight:jetty", [File.join(cwd,'jetty')])
    Rake::Task["solr:marc:index_test_data"].invoke
  end

end
