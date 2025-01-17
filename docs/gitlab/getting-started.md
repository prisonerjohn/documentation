# Getting started

This guide will demonstrate how to setup build and test automation for your Unity project hosted on gitlab using gitlab-ci.

## Overall steps

1. Understand how [gitlab-ci](https://docs.gitlab.com/ce/ci/) works.
2. Configure a license for Unity.
3. Add build scripts and integrations in your Unity project
4. Set up a gitlab-ci pipeline for your project.
5. Result: Accept merge requests with more confidence.

## First time using Gitlab CI?

Read the official documentation about [Getting started with GitLab CI/CD](https://docs.gitlab.com/ce/ci/quick_start/).

Any subsequent steps assume you have read the above.

## Supported versions

The [unity3d-gitlab-ci-example project](https://gitlab.com/gableroux/unity3d-gitlab-ci-example/) is based on [unity3d](https://gitlab.com/gableroux/unity3d) docker images from [GabLeRoux](https://github.com/GabLeRoux). Any version in the [docker hub `gableroux/unity3d` tags list](https://hub.docker.com/r/gableroux/unity3d/tags) can be used to test and build projects.

It's generally considered good practice to use the same Unity version for your CI/CD setup as you do to develop your project.

## Setting up gitlab-ci for your Unity project

### I don't have a Unity project yet

1. Fork [the unity3d-gitlab-ci-example project](https://gitlab.com/gableroux/unity3d-gitlab-ci-example/)
1. Clone the fork you just created locally
1. Continue to activation instructions

### I already have my own Unity project

1. Clone [the unity3d-gitlab-ci-example project](https://gitlab.com/gableroux/unity3d-gitlab-ci-example/)
1. Copy [`.gitlab-ci.yml`](https://gitlab.com/gableroux/unity3d-gitlab-ci-example/-/blob/master/.gitlab-ci.yml), [`Assets/Scripts/Editor/BuildCommand.cs`](https://gitlab.com/gableroux/unity3d-gitlab-ci-example/-/blob/master/Assets/Scripts/Editor/BuildCommand.cs) and [`ci` folder](https://gitlab.com/gableroux/unity3d-gitlab-ci-example/-/blob/master/ci) to your project:

   Assuming you've cloned the example project in the parent folder of your project, execute these commands from the root folder of your project:

   ```bash
   mkdir -p Assets/Scripts/Editor/
   cp ../unity3d-gitlab-ci-example/.gitlab-ci.yml ./
   cp -r ../unity3d-gitlab-ci-example/ci ./
   cp ../unity3d-gitlab-ci-example/Assets/Scripts/Editor/BuildCommand.cs ./Assets/Scripts/Editor/
   ```

1. Open and edit the [`.gitlab-ci.yml`](https://gitlab.com/gableroux/unity3d-gitlab-ci-example/-/blob/master/.gitlab-ci.yml) you copied to your project and update [the variables](https://gitlab.com/gableroux/unity3d-gitlab-ci-example/-/blob/master/.gitlab-ci.yml#L7-12) with the versions you need. Your Unity project version can be found in `ProjectSettings/ProjectVersion.txt`.
1. Continue to activation instructions
