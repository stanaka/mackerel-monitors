task :default do
  sh "mkr monitors diff -e"
end

task :kick_circleci do
  project=ENV["PROJECT"]
  branch=ENV["BRANCH"] || "master"
  circle_token=ENV["CIRCLECI_TOKEN"]

  trigger_build_url="https://circleci.com/api/v1/project/#{project}/tree/#{branch}?circle-token=#{circle_token}"

  sh "curl -X POST #{trigger_build_url}"
end

task :create_pr do
  require 'octokit'

  sh "mkr monitors pull"
  branch="bundle-update-#{`date -u "+%Y%m%d"`}"
  #sh "git config --global user.email user@eample.com"
  #sh "git config --global user.name 'your name'"
  sh "git add monitors.json"
  sh "git commit -m 'Monitor rules update'"
  sh "git branch -M #{branch}"
  sh "git push origin #{branch}"

  client = Octokit::Client.new(access_token: ENV['GITHUB_ACCESS_TOKEN'])
  client.create_pull_request(
    ENV["PROJECT"],
    ENV["BRANCH"] || "master",
    branch.chomp,
    'Monitor rules update', # Title
    ''                      # Body
    )
end
