task :default do
  sh "mkr monitors diff -e"
end

task :kick_circleci do
  project=ENV{"PROJECT"}
  branch=ENV{"BRANCH"} || "master"
  circle_token=ENV{"CIRCLECI_TOKEN"}

  trigger_build_url="https://circleci.com/api/v1/project/#{project}/tree/#{branch}?circle-token=#{circle_token}"

  sh "curl -X POST #{trigger_build_url}"
end
