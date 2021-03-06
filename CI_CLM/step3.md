## Creating the GitHub action.

Now we are going to write the code that is necessary to perform the GitHub action anytime it is triggered.
Simply open the yaml file using the command `nano CML.yaml`{{execute}} and paste the lines of code that you can find below. Once you're done with it just press `Ctrl+X` to exit, then `y` to save and `Enter`.

This is how the body of a GitHub action is defined:
* name: the name of the action that is triggered.
* on: type of action that triggers the action. In our case it is triggered anytime some changes are pushed to the repo.
* jobs: steps that will be executed in order once the action is triggered.
* runs-on: the OS on which the action will run, in this case we chose the ubuntu OS
* container: incase needed, you can also setup a specific container that has all the requirements installed. In this case, we use the container that already has the cml installed and hence this is the path of the container. We can also specify a custom container is needed (but then CML should be installed on the container manually before).
* env: in this section of the action you can define information that you might need to access or reference when writing your code. For example in this specific case we are defining the following "repo_token: ${{ secrets.GITHUB_TOKEN }}", that is necessary because whenever a workflow starts running, GitHub creates a unique GITHUB_TOKEN secret you can use to authenticate in a workflow run, and it is not possible to run a workflow without that for security reasons. 

The remaining lines define the steps that are run:
* actions/checkout@v2 -> this is a standard action that is performed anytime an action is triggered, to setup the working directory for the code.
* pip install -r requirement.txt -> this will simply install the required libraries for our code to run
* python main.py -> this will run the code contained in main.py.

<pre class="file" data-filename="workflow.yml" data-target="prepend">
name: CI-with-CML
on: [push]
jobs:
  run:
    permissions: write-all
    runs-on: ubuntu-latest
    # optionally use a convenient Ubuntu LTS + DVC + CML image
    container: docker://dvcorg/cml-py3:latest
    steps:
      # may need to setup NodeJS & Python3 on e.g. self-hosted
      # - uses: actions/setup-node@v2
      #   with:
      #     node-version: '16'
      # - uses: actions/setup-python@v2
      #   with:
      #     python-version: '3.x'
      - uses: actions/checkout@v2
      - name: running cml
        env:
            repo_token: ${{ secrets.GITHUB_TOKEN }}
        run: |
          # Your ML workflow goes here
          pip install -r requirement.txt
          python main.py
</pre>

Now we are almost ready to trigger the action and see what we get!
