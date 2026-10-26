# 道具を揃えよう

研修を始める前に、自分のPCに必要最低限のツールを入れます。もしここで躓いたら、遠慮なく先輩を呼んでください！

## 必要なツール一覧
1. **GitHubアカウント**
2. **VS Code**
3. **Git**
4. **SourceTree**
5. **Ansible**

---

## 導入・設定の流れ

### Step 1: GitHubアカウントの作成
1. [GitHub公式サイト](https://github.com/) にアクセスし、右上の **「Sign up」** からアカウントを作成します（メールアドレス、パスワード、ユーザー名を設定）。
2. 登録完了後、ログインできることを確認しておきます。

---

### Step 2: VS Codeのインストール
1. [VS Code公式サイト](https://code.visualstudio.com/download) からインストーラーをダウンロードし、インストールします。
2. インストールが完了したら、VS Codeを起動します。

> 💡 **ここから先は、すべてVS Codeの中にある「統合ターミナル」を使って作業を進めます！**
> - **ターミナルの開き方：** VS Codeの上のメニューから `表示` ➔ `ターミナル` を選ぶ（またはショートカット `Ctrl + Shift + @` などを押す）。

---

### Step 3: Gitのインストール ＆ VS Codeターミナルでの初期設定
1. 公式サイトなどからGitをパソコンにインストールします。
2. VS Codeで開いた**統合ターミナル**に向かい、以下のコマンドを打ち込んで自分の名前とメールアドレスを登録します。

> ⚠️ **注意：メールアドレスは、必ず「GitHubに登録したものと同じ」にすること！**

```bash
git config --global user.name "あなたの名前"
git config --global user.email "あなたのメールアドレス@example.com"
```

---

### Step 4: SourceTreeのインストール ＆ GitHub連携
1. AtlassianのサイトからSourceTreeをダウンロードしてインストールします。
2. 初期設定の中で、GitHubアカウントとの連携（認証）を済ませておきます。

> 💡 **パスワード認証で弾かれる場合**
> GitHubの「Settings > Developer settings > Personal access tokens」からアクセストークンを発行し、パスワード欄にペーストしてください。

---

### Step 5: Ansibleのインストール
AnsibleはLinuxまたはMac上で動作するツールです。
Macの方はそのままでOKですが、**Windowsの方は「WSL2（Linux環境）」を準備して実行します。**

#### 🍎 Macの方
VS Codeの統合ターミナルで、以下のコマンドを実行します。
```bash
brew install ansible
```

#### 🪟 Windowsの方（WSL2 + VS Code拡張機能）
**① WSL2（Ubuntu）のインストール（初回のみ・約3分）**
1. スタートボタンを右クリック ➔ 「ターミナル（管理者）」または「PowerShell（管理者）」を開きます。
2. 以下のコマンドを1行だけ実行します。
   ```powershell
   wsl --install
   ```
3. パソコンを**再起動**します。
4. 再起動後、自動で黒い画面が開くので、任意の**ユーザー名**と**パスワード**（忘れないように！）を設定します。

**② VS Codeに「WSL拡張機能」を入れる**
1. VS Codeを開き、左側の「拡張機能アイコン（四角が4つ並んだマーク）」をクリックします。
2. 検索窓に `WSL` と入力し、Microsoft公式の**WSL 拡張機能**をインストールします。

**③ VS CodeからWSLに接続してAnsibleを入れる**
1. VS Codeの左下にある緑色のアイコン `><` をクリックし、**「WSLへの接続」**を選択します。
2. VS CodeがWSLモードで開き直したら、メニューの `表示` ➔ `ターミナル` を開きます。（※ここから先はUbuntu環境のターミナルになります）
3. 以下のコマンドを実行してAnsibleをインストールします！
   ```bash
   sudo apt update
   sudo apt install -y ansible
   ```

---

## 🎉 これで準備完了！
Windowsの方も、VS Codeの左下からWSLに接続した状態で `ansible-playbook` などのコマンドを実行すれば完璧に動きます！

すべての準備が整ったら、VS Codeでフォルダを開き、いよいよハンズオン（実践）の第1コマへ出発です！