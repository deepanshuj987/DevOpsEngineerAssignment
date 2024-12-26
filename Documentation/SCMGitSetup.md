Install Plugin if the Git option is not visible in Job Definition
1) Got to "Manage Jenkins"
2) Go to "Manage Plugins"
3) Search for "Git"
4) Install "Git" plugin for Jenkins

In the Job Selection "Definition" of Jenkins
1) Select the option "pipeline script from SCM"
2) Select "Git"
3) Add Repo URL--> "https://github.com/*"
4) Credentials "none"
5) Branch Specifier "*/main"
6) Script path "Jenkinsfile"
