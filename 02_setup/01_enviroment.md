# 道具を揃えよう

研修を始める前に、自分のPCに必要最低限のツールを入れます。もしここで躓いたら、遠慮なく先輩を呼んでください！

## 必要なツール一覧
1. **GitHubアカウント**
2. **VS Code**
3. **Git**
4. **SourceTree**
5. **Ansible**


## 導入・設定の流れ

---

### Step 1: GitHubアカウントの作成
1. [GitHub公式サイト](https://github.com/) にアクセスし、右上の **「Sign up」** からアカウントを作成します（メールアドレス、パスワード、ユーザー名を設定）。
2. 登録完了後、ログインできることを確認しておきます。

---

### Step 2: VS Codeのインストール
1. [VS Code公式サイト](https://code.visualstudio.com/download) からインストーラーをダウンロードし、インストールします。
2. インストールが完了したら、VS Codeを起動します。
   - *💡 ここから先は、すべてVS Codeの中にある「統合ターミナル」を使って作業を進めます！*
   - **ターミナルの開き方：** VS Codeの上のメニューから `表示` ➔ `ターミナル` を選ぶ（または ショートカット `Ctrl + ` ` (バッククォート)` または `Ctrl + Shift + @` を押す）。

---

### Step 3: Gitのインストール ＆ VS Codeターミナルでの初期設定
1. 公式サイトなどからGitをパソコンにインストールします。
2. VS Codeで開いた**統合ターミナル**に向かい、以下のコマンドを打ち込んで自分の名前とメールアドレスを登録します。
   - **※メールアドレスは、必ずGitHubに登録したものと同じにすること！**
   ```bash
   git config --global user.name "あなたの名前"
   git config --global user.email "あなたのメールアドレス@example.com"

---

### Step 4: SourceTreeのインストール ＆ GitHub連携
AtlassianのサイトからSourceTreeをダウンロードしてインストールします。

初期設定の中でGitHubアカウントとの連携（認証）を済ませておきます。

※パスワード認証で弾かれる場合は、GitHubの「Settings > Developer settings > Personal access tokens」からアクセストークンを発行し、パスワード欄にペーストしてください。

---

### Step 5: Ansibleのインストール

AnsibleはLinuxまたはMac上で動作するツールのpackageです。
Macの方はそのままでOKですが、**Windowsの方は「WSL2（Linux環境）」を1分で準備して実行します。**

#### Macの方
VS Codeの統合ターミナルで以下を実行します。

brew install ansible

#### Windowsの方（WSL2 + VS Code拡張機能）
1. WSL2（Ubuntu）のインストール（初回のみ・約3分）
スタートボタンを右クリック ➔ 「ターミナル（管理者）」 または 「PowerShell（管理者）」 を開きます。

以下のコマンドを1行だけ実行します。

wsl --install
パソコンを再起動します。

再起動後、自動で黒い画面が開くので、任意の ユーザー名 と パスワード（忘れないように！）を設定します。

2. VS Codeに「WSL拡張機能」を入れる
VS Codeを開き、左側の「拡張機能アイコン（四角が4つ並んだマーク）」をクリック。

検索窓に WSL と入力し、Microsoft公式の WSL 拡張機能をインストールします。

3. VS CodeからWSLに接続してAnsibleを入れる
VS Codeの左下にある 緑色のアイコン >< をクリックし、「WSLへの接続」 を選択します。

VS CodeがWSLモードで開き直したら、メニューの 表示 ➔ ターミナル を開きます。（※画面がUbuntu環境になります）

以下のコマンドを実行してAnsibleをインストールします！

sudo apt update
sudo apt install -y ansible

---

これで準備完了！Windowsの方も、VS Codeの左下からWSLに接続した状態で ansible-playbook などのコマンドを実行すれば完璧に動きます！
すべての準備が整ったら、VS Codeでフォルダを開き、いよいよハンズオン（実践）の第1コマへ出発です！