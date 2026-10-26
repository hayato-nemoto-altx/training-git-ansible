# 第2コマ：1人2役で「コンフリクト」を味わう（約30分）

ここからは、1人で「開発者A」と「開発者B」の2役を演じ、チーム開発で厄介なコンフリクト（競合）をわざと起こして解決します。

---

## Step 3. 【Aさんの作業】変数の変更とマージ
1. **ブランチを切る：** SourceTreeで `main` から新しいブランチ `feature/team-a` を生み出します。
2. **ファイルを編集：** `site.yml` の `team_name: "ベースチーム"` の部分を `"Aチーム"` に書き換えて保存します。
3. **プッシュとマージ：** コミット＆プッシュし、GitHub上で `feature/team-a` から `main` へのPull Request（PR）を作成して、**そのまま一気にマージ**します。これでAさんの変更が本筋（`main`）の正解になりました。

> [!TIP]
> **ターミナル（CLI）で行う場合**
> ```bash
> git checkout -b feature/team-a
> # (site.yml を書き換えて保存)
> git add site.yml
> git commit -m "Aチームに変更"
> git push origin feature/team-a
> ```
> ※プッシュ後はGitHub画面を開いてPRを作成・マージしてください。

---

## Step 4. 【Bさんの作業】古い状態からの変更とコンフリクト発生
1. **古い状態に戻る：** SourceTreeで `main` ブランチをダブルクリックして戻ります。

> [!WARNING]
> **超重要： ここで絶対に「Pull（最新の取得）」をしちゃダメです！** 
> あえてAさんの変更を知らない「古い状態」のまま作業を始めます。

2. **別世界を作る：** 古い `main` から、新しいブランチ `feature/team-b` を生み出します。
3. **ファイルを編集：** `site.yml` の同じ行（`team_name: "ベースチーム"`）を、今度は `"Bチーム"` に書き換えて保存します。
4. **プッシュとエラー：** コミット＆プッシュし、GitHubで `feature/team-b` から `main` へのPRを作成します。

> [!TIP]
> **ターミナル（CLI）で行う場合**
> ```bash
> git checkout main
> # ⚠️ ここで git pull は絶対にしない！
> git checkout -b feature/team-b
> # (site.yml を書き換えて保存)
> git add site.yml
> git commit -m "Bチームに変更"
> git push origin feature/team-b
> ```

**【結果】** Aさんがすでに同じ行を書き換えてマージしているため、GitHubに赤文字で **「Can't automatically merge（コンフリクト発生）」** と表示されます！これは「同時に2つの変更が存在するため、Gitがどちらを優先すればいいかわからない」というエラーです。

---

## Step 5. 【コンフリクトの解消】手動で直す技
エラーが起きたら、人間の手で解決してあげます。Ansibleはインデント（空白）のズレに鬼ほど厳しいので慎重にいきましょう！

1. **最新状態を吸い上げる：** SourceTreeで `main` をダブルクリックし、**「Pull」**を押してGitHubの最新状態（Aさんの変更）を手元のパソコンに持ってきます。
2. **自分のブランチに戻る：** 自分の作業ブランチ（`feature/team-b`）にダブルクリックで戻ります。
3. **合流させる：** SourceTreeで `main` ブランチを右クリックし、「現在のブランチに `main` をマージ」を選びます。
4. **エディタで直す：** エディタで `site.yml` を開くと、生々しい記号（`<<<<<<<` や `=======`）が書き込まれています。これらを綺麗に消して、以下のようにインデントを揃えて一つにまとめます。

```yaml
  vars:
    team_name: "AとBの合同チーム"
```

保存したら、SourceTreeでコミット（マージコミット）＆プッシュし、GitHubでPRをマージ！

> [!TIP]
> **ターミナル（CLI）で行う場合**
> ```bash
> git checkout main
> git pull origin main
> git checkout feature/team-b
> git merge main
> # (ここでコンフリクト発生！エディタで site.yml を直して保存)
> git add site.yml
> git commit -m "コンフリクト解消"
> git push origin feature/team-b
> ```

ここまでで第2コマは終了です。お疲れ様でした！