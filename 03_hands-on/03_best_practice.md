# 第3コマ：ファイルを分けて「平和」を掴むベストプラクティス（約25分）

前半戦で見た通り、全部を1個のファイルに書くからコンフリクトが起きます。後半戦は「設定値（変数）」と「タスク（手順）」のファイルを分けるやり方を実践します。

---

## Step 6. ファイルを分ける理由
- 前半のように全部を `site.yml` 1枚に書いていると、誰かがテキストをいじった瞬間にすぐ競合が起きます。
- 「チーム名などのデータ」は `group_vars/all.yml` という専用の引き出しにしまい、「実際の処理」は `site.yml` に書く。こうして**担当を分ける（関心を分離する）**のがインフラ自動化の鉄則です。

---

## Step 7. 【Aさんの作業】設定値を別ファイルに隔離する
1. **最新にする：** SourceTreeで `main` に切り替え、**「Pull」**して最新状態にします。
2. **新ブランチ：** 新しいブランチ `feature/vars` を生み出します。
3. **別ファイルを作る：** リポジトリの中に `group_vars` という名前のフォルダを作り、その中に `all.yml` というファイルを作って以下を書き込みます。

```yaml
# group_vars/all.yml
team_name: "インフラ構築チーム"
```

4. **プッシュとマージ：** コミット＆プッシュし、GitHubでPRを作ってそのままマージします！

> [!TIP]
> **ターミナル（CLI）で行う場合**
> ```bash
> git checkout main
> git pull origin main
> git checkout -b feature/vars
> # (group_vars/all.yml を作成して保存)
> git add group_vars/all.yml
> git commit -m "変数を別ファイルに分離"
> git push origin feature/vars
> ```

---

## Step 8. 【Bさんの作業】タスクを書き換える（※また古い状態から）
1. **古い状態に戻る：** SourceTreeで `main` ブランチに戻ります。（※絶対ここでPullしちゃダメ！）
2. **古い`main`からブランチを切る：** Aさんが `group_vars` を作る前の古い状態の `main` から、新しいブランチ `feature/html-task` を生み出します。
3. **`site.yml`を完全に書き換える：** `site.yml` の中身を、以下のようにHTMLを作る指示書に書き換えます（変数定義の `vars:` の部分はもう不要なので消してOKです）。

```yaml
# site.yml
- name: ローカルWebページの生成
  hosts: localhost
  tasks:
    - name: index.html を作成する
      copy:
        dest: "./index.html"
        content: |
          <!DOCTYPE html>
          <html lang="ja">
          <head>
              <meta charset="UTF-8">
              <title>Ansible テストページ</title>
          </head>
          <body>
              <h1>ようこそ！</h1>
              <p>このページは <b>{{ team_name }}</b> が自動生成しました。</p>
          </body>
          </html>
```

4. **プッシュ：** コミット＆プッシュし、GitHubでPRを作成します。

> [!TIP]
> **ターミナル（CLI）で行う場合**
> ```bash
> git checkout main
> # ⚠️ ここで git pull は絶対にしない！
> git checkout -b feature/html-task
> # (site.yml を書き換えて保存)
> git add site.yml
> git commit -m "タスクをHTML作成に変更"
> git push origin feature/html-task
> ```

---

## Step 9. 【自動マージの確認】
GitHubのBさんのPR画面を見てみてください。

Aさんがいじったのは `group_vars/all.yml`、Bさんがいじったのは `site.yml` です。ファイルが完全に分かれているため、GitHubは「競合が起きていない」と判断します！

画面に **「Able to merge（自動マージ可能）」** と表示されているはずです。そのままマージしちゃいましょう！

---

### 🌟 チャレンジ課題（余裕がある人はやってみよう！）
Bさんが書いた `index.html` の中身（HTMLのコード）を少し変えてみよう！
例えば `<h1>ようこそ！</h1>` の文字を自分の好きな言葉に変えたり、文字の色を赤くするコード（`<h1 style="color: red;">` 等）を仕込んでみよう。

ここまでで第3コマは完了です！いよいよ次がラストスパートです。