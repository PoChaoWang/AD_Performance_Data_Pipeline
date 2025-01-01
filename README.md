# Ad Performance Data Pipeline

## 專案簡介

此專案是我第一次嘗試實現資料流程與自動化，為了避免浪費您的時間，我將詳細的專案背景放在最後。
因為廣告平台的 API 需要公司資訊，但本專案只是我自己個人的專案，所以無法實現串接各大廣告後台的 API 數據，一切資料皆為使用 Chat GPT 創造的模擬數據。

### 此專案為廣告成效數據處理管線,主要功能包含:

1. Use Python to merge CSV files from a specified folder and remove duplicates.
2. Insert the processed data into a PostgreSQL database.
3. Use dbt in the staging layer to modify column names, and generate a combined file in the marts layer.
4. Schedule daily updates with Airflow.
5. Package Airflow into Docker.

![image](https://github.com/PoChaoWang/Ad_Performance_Data_Pipeline/blob/main/images/process.png)

### 此專案目的:

- 降低人工處理數據的時間成本
- 進行跨平台成效比較分析
- 優化廣告投放策略

### 技術架構:

- 程式語言: Python 3.9.6
- 資料處理: Pandas
- 資料儲存: PostgreSQL, SQLAlchemy
- 資料庫連接: psycopg2
- 檔案處理: os, glob
- 時間處理: datetime
- 排程工具: Apache Airflow
- 容器化部署: Docker 27.4.0

## 安裝說明

### Installing Docker

If Docker is not installed on your system, follow the steps below to install it:
**For Linux**

1. Update your package list:

```
sudo apt update
```

2. Install Docker using the package manager:

```
sudo apt install docker.io
```

3. Verify the installation:

```
docker --version
```

**For Mac**

1. Download Docker Desktop for Mac from the [Docker Docs](https://docs.docker.com/desktop/setup/install/mac-install/).
2. Open the downloaded .dmg file and follow the installation instructions.
3. Start Docker Desktop and verify the installation by running:

```
docker --version
```

**For Window**

1. Download Docker Desktop for Windows from the [Docker Docs](<[https://docs.docker.com/desktop/setup/install/mac-install/](https://docs.docker.com/desktop/setup/install/windows-install/)>).
2. Open the downloaded .dmg file and follow the installation instructions.
3. Start Docker Desktop and verify the installation by running:

```
docker --version
```

### ETL Script

The file path: elt
