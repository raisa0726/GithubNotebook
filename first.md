# はじめる

1. [新規作成](#新規作成)
2. [リポジトリから取得](#リポジトリから取得)
3. [他の人の変更をローカルに取り込んで試したい時](#他の人の変更をローカルに取り込んで試したい時)

## 新規作成

1. 新しいリポジトリを作成する。
2. トークンの取得
  [資料を参考に行う](https://docs.github.com/ja/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)
  以下のような場合に使用する。発行されたパスワードはメモしておくこと。

    ```bash
    # httpの場合
    $ git clone https://github.com/username/repo.git

    # sshの場合
    $ git clone リンク
        Username: your_username
        Password: your_token #ここに入力する
    ```
3. gitconfigの編集

    ```bash
    git config --global user.name ユーザー名
    git config --global user.email 登録しているメールアドレス
    git config --global user.password sshのトークン
    ```
4. ターミナルでGithubにアップしたいディレクトリに移動する。
5. 下記コマンドを実行

    ```bash
    git init

    #はじめなのですべて選択することが多い
    git add -A

    # git add を取り消すときは git reset
    git commit -m "first commit"
    git remote add origin GithubのリポジトリURL

    #リモートリポジトリへ登録してpush
    git push -u origin main

    # 登録済みの場合
    git push
    ```

## リポジトリから取得

1. ターミナルでGithubにアップしたいディレクトリに移動する。
2. 下記コマンドを実行

    ```bash
    git clone cloneしたいリポジトリURL
    # ブランチを指定する場合は下
    git clone -b ブランチ名 リポジトリのURL
    cd リポジトリ名
    ```

## 他の人の変更をローカルに取り込んで試したい時

1. リモートの特定のブランチをローカルに取り込む(pullするより安全)

    ```bash
    # 新しいプロジェクト
    git fetch origin 試したいブランチ名

    # forkされたbranchを取り込む
    git remote add ブランチリンク
    git remote set-url リモート名 git@github.com:ユーザー名/プロジェクト名.git

    # 状況確認
    git remote -v
    ```
2. 取り込んだブランチに移動

    ```bash
    git checkout 移動先のブランチ名
    ```
3. リモート追跡のmainに強制的に合わせる

    ```bash
    git reset --hard origin main
    ```

## Branchの作成

1. 新しいブランチを作る時は他の変更がMergeされているかもしれないので必ずpullで更新する(Cloneした直後を除く)

    ```bash
    git pull
    ```
2. ブランチを作成しつつ、そのブランチに移動する

    ```bash
    git checkout -b 新しいブランチ名
    ```
