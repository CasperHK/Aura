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

| 模組 | Laravel 對應 | 功能描述 |
|---|--------|----------|----------|
| Aura Core | Routing / Controllers | 統一調度中心，管理應用的生命週期。 |
| Aura Pulse | Eloquent ORM | AI 的數據管理層，將 RAG 與向量庫抽象化。 |
| Aura Vision | Middleware | 圖像識別與影像串流處理插件。 |
| Aura CLI | Artisan | 基於 uvx 的強大工具：`aura make:soul` |

## 🚀 快速啟動 (Powered by [uv](https://docs.astral.sh/uv/))
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
├── k8s/                 # Kubernetes 資源清單 (YAML)
├── openshift/           # OpenShift 特定配置 (Route, SCC, Template)
├── helm/                # Helm 圖表及部署配置
├── Dockerfile           # 容器化配置
├── pyproject.toml       # uv 專案配置文件
└── .env                 # API 金鑰與模型參數
```

## 🐳 Kubernetes & OpenShift 原生支援

Aura 完全支援 Kubernetes 和 OpenShift 部署，提供生產級別的容器化方案。

### 快速部署 (Kubernetes)

**前置需求**
- Kubernetes 叢集 (v1.24+)
- kubectl 客戶端
- 可選：Helm 3.0+

**使用 kubectl 部署**
```bash
# 1. 部署到 Kubernetes
kubectl apply -f k8s/namespace.yaml
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/secret.yaml
kubectl apply -f k8s/rbac.yaml
kubectl apply -f k8s/pvc.yaml
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl apply -f k8s/hpa.yaml
kubectl apply -f k8s/ingress.yaml

# 2. 檢查部署狀態
kubectl get pods -n aura
kubectl get svc -n aura

# 3. 查看日誌
kubectl logs -n aura -f deployment/aura-core
```

**使用 Helm 部署 (推薦)**
```bash
# 1. 部署到 Kubernetes
helm install aura ./helm/aura \
  --namespace aura \
  --create-namespace \
  --values helm/aura/values.yaml \
  --set secrets.OPENAI_API_KEY=your-key \
  --set secrets.ANTHROPIC_API_KEY=your-key

# 2. 檢查部署狀態
helm status aura -n aura

# 3. 升級版本
helm upgrade aura ./helm/aura -n aura

# 4. 卸載
helm uninstall aura -n aura
```

### OpenShift 部署

**使用 OpenShift Template 部署**
```bash
# 1. 建立新專案
oc new-project aura

# 2. 部署應用
oc apply -f openshift/scc.yaml
oc process -f openshift/template.yaml \
  -p PROJECT_NAME=aura \
  -p IMAGE_REGISTRY=docker.io \
  -p IMAGE_NAMESPACE=library \
  -p IMAGE_TAG=latest \
  -p REPLICAS=3 | oc apply -f -

# 3. 檢查路由
oc get routes -n aura

# 4. 查看日誌
oc logs -f deployment/aura-core -n aura
```

**使用 Helm 部署到 OpenShift**
```bash
# 使用 OpenShift 特定設定
helm install aura ./helm/aura \
  --namespace aura \
  --create-namespace \
  --values helm/aura/values.yaml \
  --set openshift.enabled=true \
  --set ingress.enabled=false \
  --set secrets.OPENAI_API_KEY=your-key
```

### 容器映像

**構建自訂映像**
```bash
# 使用 Dockerfile 構建
docker build -t aura:latest .

# 推送到登錄檔
docker tag aura:latest your-registry/aura:latest
docker push your-registry/aura:latest
```

### 環境配置

通過 `k8s/configmap.yaml` 和 `k8s/secret.yaml` 管理環境變數：

**ConfigMap (公開設定)**
- `MODEL_PROVIDER`: LLM 提供者 (openai, anthropic, llama)
- `VECTOR_DB_TYPE`: 向量資料庫 (qdrant, pinecone)
- `LOG_LEVEL`: 日誌級別

**Secret (敏感資訊)**
- `OPENAI_API_KEY`: OpenAI API 金鑰
- `ANTHROPIC_API_KEY`: Anthropic API 金鑰

**更新配置**
```bash
# 編輯 ConfigMap
kubectl edit configmap aura-config -n aura

# 編輯 Secret (使用密封化秘密)
kubectl create secret generic aura-secrets \
  --from-literal=OPENAI_API_KEY=your-key \
  --dry-run=client -o yaml | kubectl apply -f -
```

### 資源要求與限制

默認配置：
- **請求 (Request)**: CPU 250m, Memory 256Mi
- **限制 (Limit)**: CPU 1000m, Memory 1Gi

自動擴展 (HPA)：
- 最小副本數: 3
- 最大副本數: 10
- CPU 目標: 70%
- Memory 目標: 80%

### K8s 資源清單說明

| 檔案 | 用途 |
|------|------|
| `namespace.yaml` | 建立 Aura 命名空間 |
| `configmap.yaml` | 應用配置 (環境變數) |
| `secret.yaml` | 敏感資訊 (API 金鑰) |
| `deployment.yaml` | Pod 部署策略與副本管理 |
| `service.yaml` | 網路服務與服務發現 |
| `rbac.yaml` | 角色與權限配置 |
| `pvc.yaml` | 永久存儲聲明 |
| `hpa.yaml` | 自動水平擴展 |
| `ingress.yaml` | 外部流量入口 |

### OpenShift 資源清單說明

| 檔案 | 用途 |
|------|------|
| `route.yaml` | OpenShift 路由 (取代 Ingress) |
| `scc.yaml` | 安全上下文限制 |
| `template.yaml` | 可參數化的 OpenShift 範本 |

### 故障排查

**檢查 Pod 狀態**
```bash
kubectl describe pod -n aura <pod-name>
kubectl logs -n aura <pod-name>
```

**驗證健康檢查**
```bash
kubectl exec -it -n aura <pod-name> -- curl http://localhost:8000/health
```

**查看事件日誌**
```bash
kubectl get events -n aura --sort-by='.lastTimestamp'
```

## 🤝 參與貢獻
Aura 的目標是讓 AI 開發平民化。
* GitHub: github.com
* Discord: Join our developer community

---

## 🚀 部署與生產環境

Aura 完全原生支援 Kubernetes 和 OpenShift，提供企業級容器化部署。詳見上方「Kubernetes & OpenShift 原生支援」章節。

---

## 📄 授權
本項目採用 MIT License 授權。
給開發者的 Tip：
使用 uv 後，您可以利用 `uv lock` 確保您的 AI 應用在開發環境與生產環境（Docker）中的依賴完全一致，徹底解決「在我電腦上能跑」的 AI 部署難題。
