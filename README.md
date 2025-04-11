# exploring actions
we will be learning github actions
- a robust automation tool that empowers you to streamline repetitive tasks
- automate your software development workflows
- enhancing productivity and code quality


## workflows
- `set up job` and `complete job` are the steps that gets added automatically
- during `set up job`, any `actions` used in workflow is downloaded from marketplace

## actions:
- actions in github workflow are prebuilt, reusable, automation components designed for specific tasks
- https://github.com/marketplace?type=actions
- types of actions:
    - github verified actions
    - third-party/ community actions

- defining action version can be done in 3 ways
    - tags
        - actions/checkout@v4.2.2
    - branches
        - actions/checkout@main 
    - SHAs
        - actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683

- any files which are generated or created during the workflow execution are automatically deleted when the vm closes

- disable workflow if not in use

## workflow with multiple jobs
- jobs will be running in parallel by default, they do not wait for any other job 
- each job runs on different runner

### execute multiple jobs in sequence using `needs` syntax

### storing workflow data as artifacts
- upload from one job 
    - `actions/upload-artifact@v4`
- download in another job
    - `actions/download-artifact@v4`

### variables and secrets
- environment variables can be stored at three different places
    - step level
    - job level
    - workflow level
        - can be used in following ways:
            - $variable_name
            - ${{ env.variable_name }}
    - repository level
        - `settings` of the project -> `secrets and variables` -> `actions` -> `new repository variable`
       - can be used in following way:
            - ${{ vars.VARIABLE_NAME }} 

### working with secrets
- secrets can be stored at 
    - organization level
    - repository level
        - `settings` of the project -> `secrets and variables` -> `actions` -> `new repository secret`

        - use in the workflow as:
            - ${{ secrets.SECRET_NAME }}
    - environment level

## triggering a workflow

https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows

- `workflow_dispatch` # adds a button to manually trigger a workflow

## using job concurrenty
- when a long running deploy job is in progress, you don't want another deploy job to run at the same time
- https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/control-the-concurrency-of-workflows-and-jobs
    - `concurrency` key ensures that only one workflow runs or a job is in progress. we can use the key at the workflow level and at the job level 
    - `cancel-in-progress` 
        - if `true` cancels any current running job or workflow within the same concurrency group  
        - if `false` new one waits till the currently running job completes

### timeout for jobs and steps
- github by default kills the workflow after 6hrs
- timeout option can be mentioned at
    - step level
    - job level

## using matrix strategy
