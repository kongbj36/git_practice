GitとGitHubの使い方整理

1_gitの初期設定
１）git --version
バージョン確認及びgitが設置されているか確認

2_gitユーザー、メールの設定
$ git config --global user.emal "kongbj36@gmail.com"
$ git config --global user.name "kongbj"

3_gitのinit
最初にgitを使う時
$ git branch -m main
＊以下のコードを設定すると該当pcはinitをするとき、毎回mainを基本ブランチにする。
$ git config --global init.defaultBranch main

4_**********addとcommitの基本使用方法**********
➀ファイルを修正→➁「$ git add .」 または「$ git add filename1 filename2 filename3」→➂「$ git commit -m 'コミットするバージョンのコメント'」

5_add及びcommitの状態確認
$ git log：コミットの履歴を確認可能
$ git status：現在のgit addとcommitなどの状態を確認
$ git log --all --oneline：簡単にコミット名だけ表示
$ git log --oneline --graph
*最近はgit bashでgitを操作するより、editorを使用するのか普通になっている。

6_基本使用以外の重要なコマンド
$ git restored --staged ファイル名
addしてステージングにあるファイルをステージングから外す。

7_**********commitの比較(diff)**********
普通にgitにある機能としては
$ git diff コミットid1 コミットid2
の方法があるが、これはインターフェイスが良くないので、VScodeを使用すると「Git graph」などのGUIツールを使用する。

8_**********branchの基本使用方法**********
1)branchの生成
$ git branch ブランチ名
2)branch間の移動
$ git swithch 移動するブランチ名
3)現在のbranch確認
$ git status
4)merge(生成したbranchを親branchにmergeする)
ex)mainブランチから生成したabcブランチをmergeする
➀mainブランチに移動「$ git switch main」→➁「$ git merge abc」→➂「git log --graph」などで確認
5)conflict解決
➀conflict部分を修正→➁修正して完成した部分をstageに上げる「git add ファイル名」→➁git commit -m 'コミット内容説明'

8-1_branchする方法4つ
1)3-way: 一番基本的なmerge方法
2)fast-forward: 基準のブランチ（例えばmainブランチ）に変更内容がない時、mergeすると「自動的」にfast-forwardマージをする。
3)squash
4)rebase
*マージの方法はプロジェクトのチームのルールに合わせてする。

8-2_マージ後に作業したbranchの削除
$ git branch -d ブランチ名
もし、作業しているブランチをマージしなくて削除したいときは強制的に削除する必要がある。
$ git branch -D ブランチ名

9_指定したコミットに移動
restore, revert, reset
| コマンド      | 目的           　　　　　　 | 履歴への影響   　 | 使用場面                   　　　　　　　| 安全性（共同作業）
| ------------- | ------------------------- | ------------------ | ---------------------------------------- | ------------- 
| `git restore` | 作業中の変更を元に戻す   　| ❌        　　　　 　| 編集ミスを取り消す              　　　　　| 安全            
| `git revert`  | コミットを打ち消す     　　| ✅（追加される）  　| 間違ったコミットを戻す（履歴を保ちたい場合） | 安全（推奨）        
| `git reset`   | 履歴を巻き戻す／変更を破棄 | ✅（履歴が変わる） 　| ローカルの履歴を消したいとき（慎重に！）   | 危険（基本的にローカル用） 



