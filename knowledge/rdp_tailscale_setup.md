# 外出先からWindows PCへRDP接続する環境構築手順書

## 全体構成のイメージ
- **iPhone**：Tailscaleに接続し、Siriショートカット経由でRaspberry PiにSSHコマンドを送信。  
- **Raspberry Pi**：常時Tailscaleネットワークに参加し、受け取ったコマンドでWake on LAN (WoL)を実行しWindows PCを起動。  
- **Windows PC**：WoLで起動後、自動的にTailscaleに参加。  
- **クライアント端末（iPhone/iPad/ノートPCなど）**：Tailscaleネットワークに接続し、Windows PCのTailscale IPに対してRDP接続を実行。  

---

## 構築手順

### 1. Tailscale環境の準備
1. **アカウント作成**：Tailscale公式サイトでアカウントを作成。  
2. **Raspberry Piにインストール**
   ```bash
   curl -fsSL https://tailscale.com/install.sh | sh
   sudo tailscale up
   ```
   → 常時Tailscaleネットワークに接続しておく。  
3. **Windows PCにインストール**  
   - Tailscaleクライアントをインストールし、自動起動設定にする。  

---

### 2. ネットワーク設定
1. **Windows PCのIP固定**：家庭内ルーターでDHCP予約し、固定IPを割り当てる。  
2. **Raspberry PiのIP固定**：家庭内LANでも固定にしておく（自宅からショートカットで起動する用途向け）。  

---

### 3. Wake on LAN設定
1. **Windows PCのBIOS/UEFIでWoLを有効化**。  
   - 「Wake on LAN」「PCI-E Wake」などの項目を有効にする。  
2. **OS側で設定**
   - デバイスマネージャー → ネットワークアダプタ → 電源管理で「Magic Packetでのみスリープ解除を許可」を有効化。  
3. **Raspberry PiにWoLスクリプトを設置**
   - `wol.sh` 例：
     ```bash
     #!/bin/bash
     # Windows PCのMACアドレスを指定
     wakeonlan 00:11:22:33:44:55
     ```
   - `wakeonlan` パッケージをインストールして利用。

---

### 4. iPhone側の準備
1. **Tailscaleアプリをインストール**し、ネットワークに参加。  
2. **SSH鍵ペア作成（iPhone上で）**
   - Siriショートカットが許容する方法で鍵生成。  
   - 公開鍵をRaspberry Piの `~/.ssh/authorized_keys` に追加。  
3. **Siriショートカット作成**
   - 「SSH接続」アクションを追加。  
   - 実行コマンドに `bash ~/wol.sh` を指定。  

---

### 5. リモートデスクトップ接続
1. Windows PCが起動すると自動的にTailscaleに接続される。  
2. クライアント端末（外出先のノートPCやiPhone/iPadなど）をTailscaleに接続。  
3. RDPクライアントアプリを使用し、Windows PCのTailscale IPに接続。  
   - Windows側は「リモートデスクトップ接続の許可」をあらかじめ有効化しておく必要あり。  

---

## 注意点
- **SiriショートカットのSSH鍵**はiPhone自身で生成したものしか使用できないため、他の鍵を流用不可。  
- **Tailscaleは暗号化トンネルを利用**するので、ポート開放やDDNSは不要。  
- **Windows側の電源設定**は、スリープや休止状態からWoLで起動できるように調整しておく。  
