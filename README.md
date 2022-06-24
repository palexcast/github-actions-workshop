# Welcome to the GitHub Actions workshop!

You will only be required to change code in the folder `.github/workflows` for the first few tasks.

## Tasks
### Task 1 - Fix the broken workflow

__File:__ `.github/workflows/task_1_broken.yml`

1. __The workflow is broken. Fix it.__

When it is working you should see a green checkmark in the GitHub Actions status beside the action `Task 1 - Fix the broken workflow`

Look at the error message in the GitHub Actions log to discover what is wrong. Often GitHub Actions will indicate syntax errors in the workflow file.

### Task 2 - Optimize the workflow

__File:__ `.github/workflows/task_2_optimize.yml`

1. __Copy the contents of your finished task 1 workflow file into this file.__

2. __Change the name to `Task 2 - Optimizing the workflow`__

We won't be updating the workflow to be more performant as in terms of cost, but in terms of visibility.

The workflow will exit at the earliest failure, so it will not run all steps, hiding some errors.

We want there to be three jobs, `Lint`, `Test` and `Build`. 

This way, if there are any errors in each of the steps, it will be quick to discover what went wrong.


### Task 3 - Creating a workflow Chuck Norris would be proud of

__File:__ `.github/workflows/task_3_quote_of_the_day.yml`

1. __Create a new workflow file named `task_3_quote_of_the_day.yml`__
2. __This workflow should trigger on the event `workflow_dispatch`, [read more here](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_dispatch).__

3. __Setup a new job that uses these steps to output a Chuck Norris Joke.__

```
      - name: Fetch quote
        uses: fjogeleit/http-request-action@v1
        id: getQuoteResponse
        with:
          url: 'https://api.chucknorris.io/jokes/random'
          method: 'GET'
      - name: Show Response
        id: quote
        run: |
          echo "::set-output name=QUOTE::${{ fromJson(steps.getQuoteResponse.outputs.response).value }}"
```

5. __Use [this action](https://github.com/marketplace/actions/http-request-action) to perform a http `POST` request to `https://chuck.alexc.no/api/quote`.__
__The body should be as follows__ 
```
{ "quote": "<the quote here>", "accessCode": "<ask Alex for the code>" }
```

The accessCode is secret, and should be treated as such! See this link for information on [how to create a secret](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository)
and this link on [how to use a secret in your workflow](https://docs.github.com/en/actions/security-guides/encrypted-secrets#using-encrypted-secrets-in-a-workflow).

The quote can be fetched from the step with `id: quote`, look [here for more info](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#example-setting-a-value).


5. __View the glorious results [here](https://chuck.alexc.no).__ 

We won't be updating the workflow to be more performant as in terms of cost, but in terms of visibility.

The workflow will exit at the earliest failure, so it will not run all steps, hiding some errors.

We want there to be three jobs, `Lint`, `Test` and `Build`.

This way, if there are any errors in each of the steps, it will be quick to discover what went wrong.


### Task 4 - Create a composite action

__File:__ `.github/workflows/task_4_composite_action.yml`

1. __Create a new workflow file named `task_4_composite_action.yml`__
2. __Create a composite action locally, following [these instructions](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action)__
3. __The action should take an input `accessCode` and perform the same steps as the previous task with this input.__
4. __Edit the workflow `task_4_composite_action.yml` so that it uses your new action!__


### Task 5 - Create your own workflow that listens to the [issue comment event](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#issue_comment)

Use the [marketplace](https://github.com/marketplace?type=actions) to find actions that help you respond to comments. 
Try to make it react with an emoji, or respond to the comment with a message.

### Task 6 - Creating a ChatOps Bot

You can dispatch your own repository events in GitHub Actions. These can be useful to trigger other workflows who are listening to the same event.

Use this repository as inspiration to get started. https://github.com/peter-evans/slash-command-dispatch