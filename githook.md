To create a pre-commit hook using Bash, you can follow these steps:

1. **Create a Bash script**: Write a Bash script that performs the checks you want to run before a commit. For example, if you want to check for the presence of "TODO" comments in the code, you could create a script like this:

   ```bash
   #!/bin/bash

   if git diff --cached | grep -q 'TODO'; then
       echo 'Your commit contains TODO comments. Resolve them before committing.'
       exit  1
   fi
   ```

   Save this script in your repository, for example as `pre-commit.sh`, and make sure it's executable (`chmod +x pre-commit.sh`).

2. **Create a `.git/hooks` directory**: If it doesn't exist already, create a `.git/hooks` directory in your repository. This is where Git will look for your hooks.

3. **Create a pre-commit hook**: In the `.git/hooks` directory, create a file called `pre-commit` (without any extension). This will be your pre-commit hook. Make it executable (`chmod +x .git/hooks/pre-commit`).

4. **Link the Bash script**: In the `pre-commit` hook file, add a line to call your Bash script. For example:

   ```bash
   #!/bin/sh
   ./.git/hooks/pre-commit.sh
   ```

   This will run your Bash script every time a commit is attempted.

5. **Share the repository**: When someone clones your repository, they will need to set up the hook manually by creating the `.git/hooks` directory and linking the `pre-commit` hook to your script.

6. **Automate hook installation**: To make it easier for others to set up the hook, you can provide a script that automates this process. Here's an example script you could include in your repository:

   ```bash
   #!/bin/bash

   cd .git/hooks
   if [ ! -f pre-commit ]; then
       cat << 'EOF' > pre-commit
   #!/bin/sh
   ./.git/hooks/pre-commit.sh
   EOF
       chmod +x pre-commit
   fi
   ```

   Save this script as `install-hooks.sh` and make it executable. Team members can run this script to automatically set up the pre-commit hook in their local repository [4].

Remember to commit and push the `pre-commit.sh` and `install-hooks.sh` scripts to your repository, so that they are available to others who clone your repository.