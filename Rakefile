require 'rubygems'
require 'rake'
require 'rspec/core/rake_task'
require 'yaml'
require 'jasmine'
require 'coffee-script'
require 'bundler/gem_tasks'
load 'jasmine/tasks/jasmine.rake'

desc 'Run RSpec'
RSpec::Core::RakeTask.new do |t|
  t.verbose = false
end

task default: [:spec, 'compile_js', 'jasmine:ci']

def compile_coffee_script(file, path)
  source = File.read File.expand_path("#{path}/#{file}.coffee", __FILE__)
  compiled_path = File.expand_path("#{path}/compiled/", __FILE__)
  unless File.exist?(compiled_path) && File.directory?(compiled_path)
    Dir.mkdir compiled_path
  end
  destination = File.open File.join(compiled_path, file), 'w+'
  destination.write CoffeeScript.compile(source)
end

desc 'Compile coffeescript'
task :compile_js do
  compile_coffee_script('danthes.js', '../app/assets/javascripts')
  compile_coffee_script('danthesSpec.js', '../spec/coffeescripts')
end
