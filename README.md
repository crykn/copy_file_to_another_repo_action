# copy_folder_to_another_repo_action
This GitHub Action copies a folder from the current repository to a location in another repository

# Example Workflow
    name: Push File

    on: push

    jobs:
      copy-file:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout
          uses: actions/checkout@v2

        - name: Pushes test folder
          uses: crykn/copy_folder_to_another_repo_action@v1.0.5
          env:
            API_TOKEN_GITHUB: ${{ secrets.API_TOKEN_GITHUB }}
          with:
            source_folder: 'test_files'
            destination_repo: 'dmnemec/release-test'
            destination_folder: 'test-dir'
            user_email: 'devin.nemec@gmail.com'
            user_name: 'dmnemec'
            commit_msg: '[GHA] Update the test files.'

# Variables
* source_folder: The folder to be moved.
* destination_repo: The repository to place the folder in.
* destination_folder: [optional] The folder in the destination repository to place the file in, if not the root directory.
* user_email: The GitHub user email associated with the API token secret.
* user_name: The GitHub username associated with the API token secret.
* destination_branch: [optional] The branch of the source repo to update, if not master.
* destination_branch_create: [optional] A branch to be created with this commit, defaults to commiting in `destination_branch`
* commit_msg: [optional] The commit message to use.

# Behavior Notes
The action will remove the destionation folder before recreating it to place any copied files in it.
