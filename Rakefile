require 'bundler'
require 'rake'
require 'rake/testtask'

Bundler::GemHelper.install_tasks

desc "Updates the json-schema common test suite to the latest version"
task :update_common_tests do
  unless File.read(".git/config").include?('submodule "test/test-suite"')
    sh "git submodule init"
  end

  puts "Updating json-schema common test suite..."

  begin
    sh "git submodule update --remote --quiet"
  rescue StandardError
    STDERR.puts "Failed to update common test suite."
  end
end

Rake::TestTask.new do |t|
  t.libs << "."
  t.warning = true
  t.verbose = true
  t.test_files = FileList.new('test/*_test.rb')
end

task :default => :test
