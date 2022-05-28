# 作業を完了する

## 目次

1. [Mergeまでの流れ](#Mergeまでの流れ)
2. [branchのMerge](#branchのMerge)
3. [branch削除](#branch削除)
4. [コンフリクト](#コンフリクト)

## Mergeまでの流れ

1. 下記コマンドを実行し、変更をリモートブランチへ反映

  ```bash
  #すべて追加（非推奨）
  git add -A
  #変更があったすべてのファイル
  git add .
  # ファイルを指定して上げる（推奨）
  git add filename

  # 指定したファイルをコミット用のインデックスに追加
  git commit -i ファイル

  git commit -m "コメント"

  git push -u origin ブランチ名
  ```

  <details><summary>git commit のオプション</summary>

  |オプション|意味|
  |--|--|
  |-a(-all)|作業ツリー上で「変更された」か「削除された」ファイルを、自動的にインデックスにステージしてコミットを作成|
  |-amend|現在のブランチの先頭のコミットを訂正するようにコミットを作成|
  |-m|コミットメッセージを指定(指定しないとエディタで入力するためこれをすると早い)|
  |-v|エディタが起動されたときに変更点が表示される|

  </details>

2. Githubのリポジトリのページへ移動
3. 題名と内容を記入して、プルリクエストを作成
4. コードレビューをしてもらい、修正が必要であれば修正を行い、1.のコマンドを行いそれをコメントに記入する
5. 修正が完了したら下記コマンドまたはGithub上のボタンからMergeをする

    ```bash
    git checkout main
    git merge 作業ブランチ名
    ```
6. Mergeの後は必ずブランチ削除

## branchのMerge

- developへ

  ```bash
  # featureブランチからdevelopへ移動
  git checkout develop

  # featureブランチをdevelopへマージ
  git merge feature/任意の名称

  # featureブランチ削除
  git branch -d feature/任意の名称
  ```

- mainへ

  ```bash
  # mainブランチへ移動
  git checkout main

  # developブランチをmainブランチに取り込む
  git merge develop

  git push origin main
  ```

## branch削除

  ```bash
  git branch -d 消したいブランチ名

  # commitしていないものもまとめて消す
  git branch -D 消したいブランチ名
  ```

## コンフリクト

ファイル上で「自分の作業」と「他人の作業」が重複してしまった状態のこと

### 操作ミスによるコンフリクト

  ```bash
  git commit -am 'Conflicts resolved'
  ```

### コンフリクト解消方法

1. マージ先のファイルを最新の状態にする(mainがマージ先だとする)

    ```bash
    git checkout main
    git pull origin main
    ```
2. 作業ブランチ(a_branch)にmainをマージする

    ```bash
    git checkout feature#1001
    git merge main
    ```
`git status`でコンフリクトの内容を確認できる
3. エディタで対象のファイルを修正する
