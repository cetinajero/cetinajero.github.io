require "rubygems"

desc "Build website"
task :build do
  puts "## Running: bundle exec jekyll build"
  system "bundle exec jekyll build"
  cd "_site" do
    puts "## Showing changes in _site"
    system "git status"
    puts "## Build Complete!"
  end
end

desc "Run local server"
task :serve do
  begin
    puts "## Running: bundle exec jekyll serve"
    system "bundle exec jekyll serve"
  rescue Exception => e
    puts "\n## Shutting down server"
  end
end

desc "Deploy to Github Pages"
task :deploy do
  puts "## Deploying to Github Pages"

  puts "## Generating site"
  system "bundle exec jekyll build"

  cd "_site" do
    system "git add -A"

    message = "Site updated at #{Time.now.utc}"
    puts "## Commiting: #{message}"
    system "git commit -m \"#{message}\""

    puts "## Pushing generated site"
    system "git push"

    puts "## Deploy Complete!"
  end
end

desc "Git reset commands"
namespace :reset do
  task :soft do
    puts "## Current last commit: " + `git log --oneline | head -n 1`

    puts "## Rolling back last commit (git reset --soft HEAD~1)"
    system "git reset --soft HEAD~1"

    puts "## Current last commit: " + `git log --oneline | head -n 1`
  end
end

def alias_task(tasks)
    tasks.each do |new_name, old_name|
        task new_name, [*Rake.application[old_name].arg_names] => [old_name]
    end
end

alias_task [
    [:b, :build],
    [:s, :serve],
    [:d, :deploy],
    [:rs, 'reset:soft'],
]
