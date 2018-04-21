> create directory

mkdir test && cd test

> initialize git repository & commit

touch hoge.dat
git add .
git commit -m 'initial'

> create git remote repository

git create test

> push master

git push origin master

> create staging branch

git checkout -b staging
git push origin staging

> create feature branch

git checkout master
git checkout -b feature/something

> push feature branch

touch something.dat
git add . && git commit -m 'something'
git push origin feature/something

> create pull-request to staging branch

git pull-request -b staging

> merge pull-request

git checkout staging
git merge [PR-URL]

> push merged PR

git push origin staging

> delete feature branch

git push origin --delete feature/something

> open github url to delete remote branch

git checkout master
git browse

