# Quiz questions

This is only a "quiz" in the loosest sense that it's asking questions whose
answers will be part of your grade. Please use *any resources you want*, as
long as you list those resources (e.g. peers, websites, etc.)

## Navigating logs

1. What is the SHA for the last commit made by Prof. Xanda on the branch
xanda_0000_movie_processing?
(For this and future questions, the first 5 characters is plenty - neither
Git nor I need the whole SHA.)

The SHA for the last commit made by Prof. Xanda on the branch xanda_0000_movie_processing is: 9b257

2. What is the SHA for the last commit associated with line 9 of this file?

The last commit associated to line 9 of this file is: b2ed3

3. What did line 12 of this file say in commit d1d83?

Line 12 said: "2. I should really finish writing this."

4. What changed between commit e474c and 82045?

Two changes were made to the file process_movie_data.py

The line:        gross_sort = lambda x : x["Gross"]
Was changed to:  gross_sort = lambda x : int(x["Gross"])
And, the line:   top_five = rows[:-5:-1]
Was changed to:  top_five = rows[:-6:-1]

## Predicting merges

Assume at the start of each of these three questions that your
branch for switching to a top-10 list was called `top_ten`
and your branch generalizing to any number of movies was called `top_N`.
Predict the behavior of these three possible operations - you don't
have to provide a full `diff` but you should describe at a high level
what changes would happen.

These questions are supposed to be separate paths, not cumulative;
for example, you should *not* assume that the operations of 5 were run
before 6. When testing outcomes later in the lab, you should make sure to
revert back to the state of the branch before you started these questions.

5. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git merge top_N
```

The branch test would take in all the changes made to top_N. This will be done using a Fast Forward merge, as top_N is tracking test.

6. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout top_ten
git merge test
```

Here top_ten would take in the "changes" made to the branch test. It will do this using the recursive approach, and works because top_ten tracks test.

7. What do you think would happen if you ran the following commands?
What branches would change, and how?
```
git checkout test
git rebase top_ten
git rebase top_N
```

Here, we encounter a merge conflict. This is because we're first rebasing top_ten onto test, which should make the branch test identical to top_ten (and works because top_ten tracks test!). The problem arises when we then try to rebase top_N onto test, as git won't know whether to keep the changes that came from the first rebase, or accept the changes coming from the second rebase. That is why we have to manually resolve the merge conflict.