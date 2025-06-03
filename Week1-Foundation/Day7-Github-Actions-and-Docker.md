Continuous Integration (CI) with Github Actions
CI is a dev practice where devs frequently merge their code changes into a central repo, after which aumated builds and tests are run.

Benefits of CI:
- Early bug detection
- Improved code quality
- Faster releases
- Reduced risk

- Github Actions: an automation platform built into github. you can create custom software dev lifecycle workflows directly in your github repo.
    - workflows are defined in yaml files and stored in the ./github/workflows directory of your repo
    - workflows are event-driven (triggered on a push to a branch, a pull request, a schedule, etc.)
    - a workflow is made up of one or more jobs
    - each job runs in its own virtual env and consists of one or more steps
    - steps can run commands or use pre-built actions

docker in CI
why docker in CI?
- consistent build env
- dependency management
- testing within the image
- conceptual: pushing to a container registry

mini project
prerequisites:
- django project must be pushed to a github repo
- docker file should be in the root of this repo
1. create a workflow directory and file
2. define the github actions workflow in django-ci.yml
3. commit and push the workflow file to github
4. observe the workflow run on github