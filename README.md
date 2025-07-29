# Azure Form Recognizer Custom Template 3.1 容器部署指南

本指南將說明如何下載、確認和啟動 Azure Cognitive Services Form Recognizer Custom Template 3.1 容器映像。

## 系統需求

- 安裝 Docker Desktop 或 Docker Engine ([Windows版本的官方下載連結](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/containers/install-run?view=doc-intel-4.0.0&tabs=custom))。請確保 Docker 已設定為支援 Linux 容器，特別是在 Windows 環境中。

- 建立[Azure Document Intelligence 資源](https://portal.azure.com/#create/Microsoft.CognitiveServicesFormRecognizer)，並準備好有效的 Azure AI Document Intelligence Endpoint URL 和 API Key。

## 部署步驟

### 步驟 1: 下載容器映像

從 Microsoft Container Registry 下載 [Form Recognizer Custom Template 3.1](https://mcr.microsoft.com/en-us/artifact/mar/azure-cognitive-services/form-recognizer/custom-template-3.1/tags) 容器映像：

```powershell
docker pull mcr.microsoft.com/azure-cognitive-services/form-recognizer/custom-template-3.1:latest
```

### 步驟 2: 確認下載成功

執行以下命令查看已下載的容器映像：

```powershell
docker images
```

您應該會看到類似以下的輸出：

```
REPOSITORY                                                               TAG       IMAGE ID       CREATED        SIZE
mcr.microsoft.com/azure-cognitive-services/form-recognizer/custom-template-3.1   latest    xxxxxxxxx      x days ago     xxxGB
```

### 步驟 3: 啟動容器映像

使用以下命令啟動容器，配置所需的資源限制（8 核心，16GB 記憶體）：

```powershell
docker run -it --rm `
  --cpus="8" `
  --memory="16g" `
  -p 5001:5000 `
  -e EULA=accept `
  -e Billing=<YOUR_ENDPOINT_URI> `
  -e ApiKey=<YOUR_API_KEY> `
  mcr.microsoft.com/azure-cognitive-services/form-recognizer/custom-template-3.1:latest
```

### 環境變數說明

- `EULA=accept`: 接受最終用戶許可協議
- `Billing=<YOUR_ENDPOINT_URI>`: 您的 Azure AI Document Intelligence Endpoint URL
- `ApiKey=<YOUR_API_KEY>`: 您的 Azure AI Document Intelligence API Key

### 步驟 4: 驗證容器正常運行

容器啟動後，您可以透過以下 URL 確認服務是否正常運行：

```
http://localhost:5001/studio
```

## 疑難排解

如遇到問題，請參考以下文件以了解 Azure AI 容器傳回的狀態和錯誤：

[Azure AI Containers FAQ - Status Messages and Errors](https://learn.microsoft.com/en-us/azure/ai-services/containers/container-faq#what-status-messages-and-errors-do-azure-ai-containers-return)

## Reference

1. [Install and run Docker containers for Document Intelligence - Azure AI services | Microsoft Learn (04/04/2025 updated)](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/containers/install-run?view=doc-intel-4.0.0&tabs=custom)

2. [Azure Document Intelligence Resource](https://portal.azure.com/#create/Microsoft.CognitiveServicesFormRecognizer)

3. [Install Docker Desktop on Windows](https://docs.docker.com/desktop/setup/install/windows-install/)

4. [Azure AI services Document Intelligence Custom Template 3.1](https://mcr.microsoft.com/en-us/artifact/mar/azure-cognitive-services/form-recognizer/custom-template-3.1/tags)

5. [Azure Document Intelligence Sample Dataset](https://github.com/Azure-Samples/cognitive-services-REST-api-samples/tree/master/curl/form-recognizer)

6. [How to run the Azure AI Vision and Azure AI Document Intelligence engine On-Premise](https://www.capturebites.com/metaserver/help/acv-afr-on-premise/)