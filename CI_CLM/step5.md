## Using CLM to visualize results in a pull request

It is very tedious to check the results on the logs of the runner at each instance. Instead, now we will try to use CLM to visualize and display the results in a file
that will show up on the pull request page. 


CML can easily display a '.md' file using the command cml-send-comment. So after running the main.py file, write the following commands

'''
echo "## Model metrics" > report.md
          cat results.txt >> report.md
          
          echo "## Plots" >> report.md
          echo "### Loss" >> report.md
          cml-publish loss.png --md >> report.md
          
          echo "### Accuracy" >> report.md
          cml-publish acc.png --md >> report.md
          
          cml-send-comment report.md
                   
'''

testing
