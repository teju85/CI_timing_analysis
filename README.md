# Introduction
Simple repo to analysis timings of CI tests of a repo. The goal is that such a
thing would provide insights into where the most time is being spent on our CI
and thus guide us in optimizing the same.

# Usage
## Download the PR information
The script `download_CI_info` uses github's graphQL API in order to download
all the PRs that have been filed in the given repo and commits against which
CI tests were run. Given below is its usage:
```
./download_CI_info <repo> <token_file> <csv_file> [<after>]
  <repo>       the github repo. Eg: https://github.com/rapidsai/cuml
  <token_file> contains the github OAuth token stored in this file, which
               will be used for authentication
  <csv_file>   output csv file
  <after>      optional tag which is the tag that is returned by github API
               to be used for pagination. You can also get this info from the
               debug spews from this script. If this is provided, the PR
               queries will only start from after this tag
```
The output of the above script is a csv file with the following format:
`PR#, author, commit, test, status, time(s)`

Example usage:
`./download_CI_info https://github.com/rapidsai/cuml ~/.github-token cuml-prs.csv`

## Analysis
Once this csv file is available, feel free to use your own approach to analyze
it. But if you want something quick, use the accompanying notebook. Just make
sure that you have updated the path to the csv file accordingly.
