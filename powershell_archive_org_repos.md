# Batch Archiving student labs

Using Windows Powershell

1. Get a list of unarchived repos

    ``` 
    gh repo list [ORG] --no-archived --limit 200 --json nameWithOwner --jq ".[].nameWithOwner" > repos.txt 
    ```

    Change limit as needed. Needs to be set.

    To run all repos at once (only do this when checking all repos)

    ```
    foreach($o in get-content "orgs.txt") { gh repo list "$o" --no-archived --limit 200 --json nameWithOwner --jq ".[].nameWithOwner" | out-file -filepath "repos.txt" -append}
    ```

2. Edit list file
    
    Manually edit the file to remove templates, demos, answers, classroom repos.

    `vim repos.txt`
    
    command: dd

    regex search: lab\d+$
    
    search: classroom, demo, sample

3. Archive listed repos

    ```
    foreach ($r in get-content "repos.txt") { gh repo archive -y "$r" }
    ```

4. Clear file

   `clear-content ".\repos.txt"`