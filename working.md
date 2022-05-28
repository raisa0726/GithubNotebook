# 作業中に使うコマンド

1. [親ブランチの変更を反映](#親ブランチの変更を反映)
2. [作業の退避](#作業の退避)
3. [同期を除外](#同期を除外)
4. [GitHubに上げたファイルを消す](#GitHubに上げたファイルを消す)
5. [branchを作り直したい](#branchを作り直したい)

## 親ブランチの変更を反映

  ```bash
  #今いるブランチ確認(親がmain, 子がdevelop)
  git branch
    main
  * develop

  # 一旦ファイルをコミットしても良いが、stashで一時的に別の場所に退避しても良い
  git stash

  # 親ブランチへ移動
  git checkout main

  # 親ブランチを最新へ
  git pull origin main

  # 子ブランチへ移動
  git checkout develop

  # マージして反映
  git merge main

  # 退避した変更を適用しなおす
  git stash pop
  ```


## 作業の退避

  ```bash
  #pullを取り消して一つ前の状態に戻すとき
  git reset --hard HEAD@{1}

  #退避
  git stash -u

  #退避した作業を見る
  git stash list
  stash@{0}: WIP on ブランチ名e#1054: xxxx

  #退避した作業を見る
  git stash apply stash@{0}

  #退避した作業を消す
  git stash drop stash@{0}

  #退避した作業を戻して、stashリストから消す
  git stash pop stash@{0}
  ```

[参考](https://qiita.com/chihiro/items/f373873d5c2dfbd03250)

## 同期を除外

### リモートブランチの場合

- gitignoreに記述

  ```bash
  #.gitignoreファイルがある場所に移動
  #なければ以下のコマンドで作成
  touch .gitignore

  #gitから削除するがパソコンからは消さない（一番使う）
  git rm --cached ファイル名

  #既にコミット、インデックスに登録している場合
  git rm --cached path/to/file
  git rm --cached -r path/to/directory

  #gitとパソコン両方から削除
  git rm ファイル名
  ```

### ローカルブランチのみ

assume-unchanged の変更は`git reset --hard`で死ぬので, 基本的には`skip-worktree`を使う.

<details><summary>skip-worktreeを使う</summary>

  ```bash
  # 除外
  git update-index --skip-worktree path/to/file

  # 除外から戻す
  git update-index --no-skip-worktree path/to/file

  # 確認
  git ls-files -v | grep ^S
  ```

</details>

<details><summary>assume-unchangedを使う</summary>

  ```bash
  #除外
  git update-index --assume-unchanged path/to/file

  #除外から戻す
  git update-index --no-assume-unchanged path/to/file

  #確認
  git ls-files -v | grep ^h
  ```

</details>

[参考](https://qiita.com/sqrtxx/items/38a506e59df67cd5d3a1)

## GitHubに上げたファイルを消す

  ```bash
  # 単体ファイル
  git rm 消したいファイル

  # フォルダ
  git rm -r -f 消したいフォルダ
  ```

## branchを作り直したい

  ```bash
  # リモートbranch削除
  git push --delete origin branch_name

  # ローカルbranch削除
  git checkout main
  git branch -d branch_name

  #確認
  git branch
  ```
