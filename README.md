# 🪐 Aura: The Elegant AI Framework for 2026
Aura 是一款為人類工程師設計的「全方位 AI 協同框架」。它利用 uv 提供極速的環境管理，並仿效 Laravel 的開發哲學，旨在將 LLM 策劃、電腦視覺 (CV) 與自主代理 (Agents) 整合進一個優雅、一致且極具生產力的開發流程中。
"Build AI at the speed of thought." — Aura 讓開發 AI 應用不再受限於複雜的環境與依賴。

---

## ✨ 為什麼選擇 Aura？
極速環境管理：全面原生支援 uv，依賴安裝比傳統 pip 快 10-100 倍。
開發者體驗 (DX)：使用連貫介面 (Fluent Interface)，代碼結構清晰優雅。
多模態一體化：內建文字、影像、聲音的統一處理抽象層。
模型不可知 (Model Agnostic)：像更換數據庫一樣輕鬆切換 OpenAI, Anthropic 或 Llama 模型。

## 🛠 Aura 生態系統
模組	Laravel 對應	功能描述
Aura Core	Routing / Controllers	統一調度中心，管理應用的生命週期。
Aura Pulse	Eloquent ORM	AI 的數據管理層，將 RAG 與向量庫抽象化。
Aura Vision	Middleware	圖像識別與影像串流處理插件。
Aura CLI	Artisan	基於 uvx 的強大工具：aura make:soul

## 🚀 快速啟動 (Powered by uv)
1. 建立專案
    使用 uv 快速初始化 Aura 專案環境：
    ```bash
    # 建立專案夾
    mkdir my-aura-app && cd my-aura-app
    
    # 使用 uv 初始化環境並安裝 Aura
    uv init
    uv add aura-framework
    ```

2. 建立你的第一個靈魂 (Soul/Agent)
    在 Aura 中，我們稱具備特定邏輯的 AI 為 Soul。建立 main.py：
    ```python
    from aura import Aura, Soul
    
    # 初始化 Aura 應用（自動讀取 .env 設定）
    app = Aura.initialize()
    
    # 定義一個具備視覺分析能力與長效記憶的 Agent
    analyst = Soul.define("DataAnalyst") \
                  .with_vision() \
                  .using_memory("qdrant") \
                  .as_expert("財務分析師")
    
    # 執行任務
    def main():
        response = analyst.execute("分析這張報表並比對去年的數據", file="./report.png")
        print(response.content)
    
    if __name__ == "__main__":
        main()
    ```

3. 運行應用
    利用 uv 極速執行：
    ```bash
    uv run main.py
    ```

---

## ⚡ 命令行工具 (Aura CLI)
Aura 提供了類似 artisan 的開發工具，直接透過 uvx 調用，無需手動配置路徑：
`uvx aura make:soul SalesExpert` — 建立新的代理邏輯文件
`uvx aura make:perceptor FaceID` — 建立自定義視覺識別器
`uvx aura migrate:memory` — 同步向量數據庫索引結構
`uvx aura serve` — 啟動本地開發面板與視覺化調試器

---

## 📂 專案結構
Aura 規範了標準目錄，讓團隊協作不再混亂：
```text
.
├── .venv/               # 由 uv 管理的極速虛擬環境
├── souls/               # AI 代理邏輯 (Agents)
├── perceptors/          # 視覺與感知模組 (CV)
├── memory/              # 向量數據庫 Schema 與遷移
├── prompts/             # 結構化提示詞 (Markdown Templates)
├── pyproject.toml       # uv 專案配置文件
└── .env                 # API 金鑰與模型參數
```

## 🤝 參與貢獻
Aura 的目標是讓 AI 開發平民化。
* GitHub: github.com
* Discord: Join our developer community

---

## 📄 授權
本項目採用 MIT License 授權。
給開發者的 Tip：
使用 uv 後，您可以利用 `uv lock` 確保您的 AI 應用在開發環境與生產環境（Docker）中的依賴完全一致，徹底解決「在我電腦上能跑」的 AI 部署難題。
