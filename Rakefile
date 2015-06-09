#!/usr/bin/env rake

require 'html/proofer'

task :default => [:test]

desc 'Runs the tests!'
task :test => :build do
  Rake::Task['run_html_proofer'].invoke
end

desc 'Builds the site'
task :build => :remove_output_dir do
  FileUtils.rm '.jekyll-metadata' if File.exist?('.jekyll-metadata')
  sh 'bundle exec jekyll build --config=_config.yml'
end

desc 'Remove the output dir'
task :remove_output_dir do
  FileUtils.rm_r('_site') if File.exist?('_site')
end

desc 'Runs the html-proofer test'
task :run_html_proofer do
  # test your out dir!
  tester = HTML::Proofer.new('./_site', {
                              :href_ignore => "#",
                              :connecttimeout => 600,
                              :typhoeus => { :ssl_verifypeer => false, :ssl_verifyhost => 0, :followlocation => true }
                            })
  tester.run
end
