# lab05

$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_TOKEN=<полученный_токен>
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
$ source scripts/activate
$ \curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles
$ echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate
$ rvm autolibs disable
$ rvm install ruby-2.4.2
$ rvm use 2.4.2 --default
$ gem install travis
$ git clone https://github.com/${GITHUB_USERNAME}/lab04 projects/lab05
$ cd projects/lab05
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab05
$ cat > .travis.yml <<EOF
language: cpp
EOF
$ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
$ cat >> .travis.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
$ travis login --github-token ${GITHUB_TOKEN}
$ travis lint
$ ex -sc '1i|<фрагмент_вставки_значка>' -cx README.md
$ git add .travis.yml
$ git add README.md
$ git commit -m"added CI"
$ git push origin master
$ travis lint
$ travis accounts
$ travis sync
$ travis repos
$ travis enable
$ travis whatsup
$ travis branches
$ travis history
$ travis show
Report
$ popd
$ export LAB_NUMBER=05
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
