# Codeowners Validator
[![Go Report Card](https://goreportcard.com/badge/github.com/mszostok/codeowners-validator)](https://goreportcard.com/report/github.com/mszostok/codeowners-validator) [![Build Status](https://travis-ci.com/mszostok/codeowners-validator.svg?branch=master)](https://travis-ci.com/mszostok/codeowners-validator)

[![forthebadge](https://forthebadge.com/images/badges/made-with-go.svg)](https://forthebadge.com) 

## Overview

The Codeowners Validator project validates the GitHub [CODEOWNERS](https://help.github.com/articles/about-code-owners/) file.

## Local Installation

`go get -u github.com/mszostok/codeowners-validator`

## Usage

![usage](./docs/assets/usage.png)

Use the following environment variables to configure the application:

| Name | Required | Default | Description |
|-----|:---------:|:--------|:------------|
| **REPOSITORY_PATH** | Yes | | The repository path to your repository on your local machine. |
| **GITHUB_ACCESS_TOKEN** | No | | The GitHub access token. Instruction for creating token can be found [here](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/#creating-a-token). If not provided then validating owners functionality could not work properly, e.g. you can reach the API calls quota or if you are setting GitHub Enterprise base URL then an unauthorized error can occur. |
| **GITHUB_BASE_URL** | No | https://api.github.com/ | The GitHub base URL for API requests. Defaults to the public GitHub API, but can be set to a domain endpoint to use with GitHub Enterprise. |
| **GITHUB_UPLOAD_URL** | No | https://uploads.github.com/ | The GitHub upload URL for uploading files. <br> <br>It is taken into account only when the `GITHUB_BASE_URL` is also set. If only the `GITHUB_BASE_URL` is provided then this parameter defaults to the `GITHUB_BASE_URL` value. |
| **CHECK_FAILURE_LEVEL** | No | `warning` | Defines the level on which application should treat check issue as a failure. Defaults to `warning`, which treats both `error` and `warning` as failure and exits with error code 2. Possible values are: `error` and `warning`. |
| **OWNER_CHECKER_ORGANIZATION_NAME** | Yes | | The organization name where the repository is created. Used to check if GitHub owner is in the given organization. |

### Exit status codes

Application exits with different statuses codes which allows you to easily distinguish error category.  

| Code | Description |
|:-----:|:------------|
| **1** | The application startup failed due to wrong configuration or internal error. |
| **2** | The application was closed because the OS sends termination signal (SIGINT or SIGTERM). |
| **3** | The CODEOWNERS validation failed - executed checks found some issues. |

## Roadmap

_Sorted with priority. First - most important._

* [ ] Possibility to execute validator online. Automatically integrates with your GitHub account and allows you to check any repository online without the need to download and execute binary locally.
* [ ] Possibility to use the GitHub URL instead of the path to the local repository.
* [ ] Offline mode - execute all checks which not require internet connection against your local repository
* [ ] Investigate the [Go Plugins](https://golang.org/pkg/plugin/). Implement if it will simplify extending this tool with other checks.
* [ ] Move to [cobra](https://github.com/spf13/cobra/) library.
* [ ] Add test coverage.
* [ ] Add support for configuration via YAML file.
* [ ] Move dep to go modules 


Checks:

* [ ] Unowned files (Not defined owners for given files) 
* [ ] Find doubles paths
* [x] File/directory does not exits
* [x] Works with teams as well
* [x] Support for private repos (see below)
* [x] User exist or not
* [x] Validate owners
  * [x] check if owner definition is valid (GitHub user, organization team, email address)
  * [x] check if GitHub owner have GitHub account
  * [x] check if GitHub owner is in the given organization
  * [x] check if Organization team exist
