
# その他

## 違うブランチの変更が入ってしまった

1. 異なる変更のIDを確認する
2. コマンドを叩く
    ```bash
    git revert 対象のID
    git push
    ```

## 機密データを上げてしまった

<details><summary>履歴からパージする方法</summary>

```bash
# 機密データを含むファイルを削除して、最新のコミットをそのままにしておく
bfg --delete-files 機密データを含むファイル

# passwords.txt にリストされているすべてのテキストについて、リポジトリの履歴にあれば置き換える
bfg --replace-text passwords.txt

# 機密データが削除されたら、変更を GitHub に強制的にプッシュする
git push --force
```
</details>

<details><summary>git filter-repoを使用する方法</summary>

```bash
# git filter-repoをインストール
brew install git-filter-repo

# 機密データを含むリポジトリのローカルコピーが履歴にまだない場合は、ローカルコンピュータにリポジトリのクローンを作成
git clone git@github.com:ユーザー名/リポジトリ名.git

# リポジトリのワーキングディレクトリに移動
cd リポジトリ

# 次のコマンドを実行 機密データを含むファイルへのパスは、ファイル名だけではなく、削除するファイルへのパスで置き換え
git filter-repo --invert-paths --path PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA

# 機密データを含むファイルを、誤って再度コミットしないようにするため、.gitignore に追加
echo "YOUR-FILE-WITH-SENSITIVE-DATA" >> .gitignore
git add .gitignore
git commit -m "Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore"

# リポジトリの履歴から削除対象をすべて削除したこと、すべてのブランチがチェックアウトされたことをダブルチェック

#リポジトリの状態が整ったら、ローカルでの変更をフォースプッシュして、GitHub リポジトリと、プッシュしたすべてのブランチに上書き
git push origin --force --all

# 機密データをタグ付きリリースから削除するため、Git タグに対しても次のようにフォースプッシュする
git push origin --force --tags
```

</details>

[参考にしたページ](https://docs.github.com/ja/github/authenticating-to-github/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

## gitconfig設定の確認

```bash
git config --list
```

## proxyの設定

- 追加する

	```bash
	git config --global http.proxy http://プロキシ名:ポート番号
	git config --global https.proxy http://プロキシ名:ポート番号
	```

- 削除する

	```bash
	git config --global --unset http.proxy
	git config --global --unset https.proxy
	```

## ssh設定方法(非推奨)

> **warning**
> こちらの方法では、proxyの設定が難しいため、大学等で使用する場合はhttpのトークンの使用で接続することを推奨します。

[GitHub に SSH で接続する](https://docs.github.com/ja/enterprise-server@3.0/authentication/connecting-to-github-with-ssh)

## ターミナルでbranchをわかるようにしたい

```bash
export PS1='\[\033[1;32m\]\u@\h\[\033[00m\]:\[\033[1;34m\]\w\[\033[00m\]\[\033[1;31m\]$(__git_ps1)\[\033[00m\]\$ '
```

## リモートブランチ

```bash
# 追加
git remote add 名前 リンク

# 削除
git remote rm 名前
```
