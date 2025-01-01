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

The file path: etl/etl_script.py

**1. 數據庫連接設定**
請根據您的實際數據庫設置在 def main() 函數中修改以下數據庫連接參數：

```
db_params = {
        'host': 'host.docker.internal  ',
        'database': 'destination_db',
        'user': 'postgres',
        'password': 'password',
        'port': '5434'
    }
```

**2. 數據檔案路徑結構**
本專案的實驗數據是放在以下結構裡，例如：raw-dat/ga/ga_fake_data_20241221.csv

```
raw-data/
    ├── ga/
    │   └── ga_fake_data_*.csv
    ├── facebook/
    │   └── facebook_fake_data_*.csv
    ├── google/
    │   └── google_fake_data_*.csv
    ├── yahoo/
    │   └── yahoo_fake_data_*.csv
    └── criteo/
        └── criteo_fake_data_*.csv
```

建議 platform 之後的結構不要做修改，只要修改 def main()裡的 base_path

```
base_path = 'raw-data'
```

**3. 自動 CSV 格式**

- 在 def **init**(self, dest_conn_string)的 table_configs 可添加你的心資料

```
'new_platform': {
    'table_name': 'new_platform_data',
    'schema': '''
        your_custom_schema_here
    ''',
    "primary_keys": ["your_primary_keys"],
    "update_columns": ["your_update_columns"]
}
```

- 確保您的 CSV 檔案放在正確的目錄：

```
raw-data/
    └── new_platform/
        └── new_platform_fake_data_*.csv
```

- 因為大多的測試檔案是用日期、活動、廣告群組作為 Primary Key，如果有特殊需求請在 def process_platform_data(self, files, platform)使用 else if

```
        if platform == 'ga':
            combined_df = combined_df.drop_duplicates(
                subset=['day', 'utm_source', 'utm_medium', 'utm_campaign', 'utm_content']
            )
        else if plaform == 'new platform'
            combined_df = combined_df.drop_duplicates(
                subset=['your column']
            )
        else:
            combined_df = combined_df.drop_duplicates(
                subset=['day', 'campaign', 'adgroup']
            )
```

### DBT

### Airflow

### Docker

## 專案背景
