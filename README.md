# To reproduce the results, please run the following command:
This is an example of a bug in pants where `--changed-since` and `--changed-dependents=transitive` do not detect a file name change.

```
git checkout dd83a04f2fd46109e001033fb3ae9d88b6c9e50a
pants test --changed-since=b8d38bcd760c953bdabceb9cff00763ac5fd3992 --changed-dependents=transitive
```
Observe that no tests are run.

Now run the tests regularly:
```
pants test ::
```
Observe that the test fails with the following error:
```
    from number import one
E   ModuleNotFoundError: No module named 'number'
```

To confirm that `b8d38bcd760c953bdabceb9cff00763ac5fd3992` was working run:
```
git checkout b8d38bcd760c953bdabceb9cff00763ac5fd3992
pants test :: --test-force
```