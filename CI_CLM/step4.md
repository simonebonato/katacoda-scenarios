## Triggering the GitHub action

At this point we can add some lines to the code that we have just written on the yaml file:

<pre class="file" data-filename="workflow.yml" data-target="prepend">
  Echo "Model Metrics"
  cat metrics.txt
</pre>

Echo simply prints out what follows inside the GitHub actions page when it is triggered (we will see shortly), while cat does the same as Echo, only with the content of the txt file.

This is how your code is supposed to look like at this point:

<pre class="file" data-filename="workflow.yml" data-target="prepend">
name: CI-with-CML
on: [push]
jobs:
  run:
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
          Echo "Model Metrics"
          cat metrics.txt
</pre>

Now, instead of committing directly to the master branch, we can create a new branch that we will call "test", in the following way:

![image](https://user-images.githubusercontent.com/63954877/166103482-01b975b7-ce24-4cc6-a2b2-8daeac577efc.png)

Next press on "Create pull request" and we will be redirected to the PR page. 
The PR is a place where it is possible to see what changes have been made to a branch of a repository, and you can discuss with your colleagues wheter or not you want you edits to be merged into the main branch.

You will probably see something like this:

![image](https://user-images.githubusercontent.com/63954877/166104196-c92ddfd9-5ebe-4727-84d7-c138d24feca9.png)

This means that the action that we have created is up and running, and if we click on "details" we can observe what is happening inside:

![image](https://user-images.githubusercontent.com/63954877/166104425-195db6d5-f232-4b68-978d-cef9133a447e.png)

You will probably recognize the names, they are the names of the functions described in the yaml file. 
If you press on "running cml" and scroll down until the end, this is what you'll see:

![image](https://user-images.githubusercontent.com/63954877/166104334-00a9a211-3c87-4e33-bfd2-2dcefdf66bd7.png)

Which is exactly what we wanted our action to print. As you can see, seeing the results of the action in this way is a bit clunky and not really informative.

In the next section we will see how to use the CML library to get much better insights!
