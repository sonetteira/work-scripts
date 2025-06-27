# Batch Archiving student labs

Using Windows Powershell

1. Get a list of unarchived repos

    ``` 
    gh repo list [ORG] --no-archived --limit 200 --json nameWithOwner --jq ".[].nameWithOwner" > repos.txt 
    ```

    Change limit as needed. Needs to be set.

2. Edit list file
    
    Manually edit the file to remove templates, demos, answers, classroom repos.

    ```vim repos.txt```
    
    command: dd

    regex search: -lab\d+$

3. Archive listed repos

    ```
    foreach ($r in get-content "repos.txt") {
    gh repo archive -y "$r"
    }
    ```

4. Remove file

    ``` rm .\repos.txt```