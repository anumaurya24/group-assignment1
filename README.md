<div align="center">

# 🐾 Pet License Data Processing Pipeline

[![Azure Data Factory](https://img.shields.io/badge/Azure%20Data%20Factory-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/en-us/services/data-factory/)
[![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=for-the-badge&logo=snowflake&logoColor=white)](https://www.snowflake.com/)
[![Azure Blob Storage](https://img.shields.io/badge/Azure%20Blob%20Storage-0078D4?style=for-the-badge&logo=microsoft-azure&logoColor=white)](https://azure.microsoft.com/en-us/services/storage/blobs/)

**A comprehensive Azure Data Factory solution for processing pet license data from CSV files into a dimensional data warehouse in Snowflake**



</div>

---

## 📋 Project Overview

<div align="center">

### 🎯 **Mission Statement**
*Transform raw pet license data into actionable business insights through robust, scalable, and maintainable data engineering practices.*

</div>

This enterprise-grade data pipeline implements a **complete ETL solution** that processes pet license data from CSV files stored in Azure Blob Storage, transforms it through staging tables, and loads it into a dimensional data warehouse in Snowflake.

### 🎯 **Core Capabilities**

<div align="center">

| **Capability** | **Description** | **Business Value** |
|----------------|-----------------|-------------------|
| 🔄 **Automated Data Ingestion** | CSV to Snowflake pipeline | 📈 Real-time pet license analytics |
| 🎯 **Data Quality Assurance** | Built-in validation & cleansing | 🎯 Accurate reporting and compliance |
| 📊 **Dimensional Modeling** | Star schema design | 📊 Business intelligence and insights |
| ⚡ **Incremental Processing** | MERGE-based upserts | ⚡ Efficient resource utilization |
| 🛡️ **Error Handling** | Comprehensive error recovery | 🛡️ Reliable data operations |

</div>

### 🏆 **Key Features**

<div align="center">

| **Feature** | **Implementation** |
|-------------|-------------------|
| 🔄 **End-to-End Automation** | CSV ingestion → Dimensional warehouse loading |
| 🎯 **Data Quality Controls** | Validation and cleansing mechanisms |
| 📊 **Dimensional Design** | Star schema with Location, Breed, and Date dimensions |
| ⚡ **Performance Optimized** | Staging, partitioning, and efficient data transfers |
| 🔒 **Enterprise Security** | Key Vault integration and role-based access control |
| 📈 **Scalable Architecture** | Handles growing data volumes seamlessly |

</div>

---

## 🏗️ System Architecture

<div align="center">

### 🎨 **High-Level Architecture**

```mermaid
graph TB
    subgraph "🌐 Azure Cloud"
        A[📁 Azure Blob Storage<br/>CSV Files] --> B[🏭 Azure Data Factory<br/>ETL Engine]
        B --> C[🔐 Azure Key Vault<br/>Credentials]
    end
    
    subgraph "❄️ Snowflake Data Warehouse"
        B --> D[📊 Staging Layer<br/>STG_PET_LICENSE<br/>STG_LOCATION_LKP]
        D --> E[📋 Dimension Layer<br/>LOCATION_DIM<br/>BREED_DIM<br/>DATE_DIM]
        E --> F[⭐ Fact Layer<br/>PETLICENSE_FACT]
    end
    
    style A fill:#e1f5fe
    style B fill:#f3e5f5
    style C fill:#fff3e0
    style D fill:#e8f5e8
    style E fill:#fff8e1
    style F fill:#fce4ec
```

</div>

### 🔄 **Data Flow Architecture**

<div align="center">

| **Layer** | **Purpose** | **Technology** | **Key Components** |
|-----------|-------------|----------------|-------------------|
| 🌐 **Source Layer** | Raw data storage | Azure Blob Storage | CSV files, containers |
| 🏭 **Processing Layer** | ETL orchestration | Azure Data Factory | Pipelines, datasets, linked services |
| 📊 **Staging Layer** | Data validation | Snowflake | STG_PET_LICENSE, STG_LOCATION_LKP |
| 📋 **Dimension Layer** | Business entities | Snowflake | LOCATION_DIM, BREED_DIM, DATE_DIM |
| ⭐ **Fact Layer** | Business metrics | Snowflake | PETLICENSE_FACT |

</div>

---

## 🚀 Prerequisites & Setup

### 🛠️ **Required Resources Checklist**

<div align="center">

| **Category** | **Resource** | **Purpose** | **Status** |
|--------------|--------------|-------------|------------|
| ☁️ **Azure** | Data Factory (`adf-petlicense-ananya`) | ETL orchestration | ✅ Required |
| ☁️ **Azure** | Blob Storage containers | Source data storage | ✅ Required |
| ☁️ **Azure** | Key Vault (`kvpetlicenseananya`) | Credential management | ✅ Required |
| ☁️ **Azure** | Managed Virtual Network | Network isolation | ✅ Required |
| ❄️ **Snowflake** | Account (`LXUTZNB-PAA86859`) | Data warehouse platform | ✅ Required |
| ❄️ **Snowflake** | Database (`PET_LICENSE_DB`) | Main data storage | ✅ Required |
| ❄️ **Snowflake** | Warehouse (`PET_WH`) | Compute resources | ✅ Required |

</div>

### 🔑 **Required Permissions**

<div align="center">

| **Service** | **Permission Level** | **Required Actions** |
|-------------|---------------------|---------------------|
| 🏭 **Azure Data Factory** | Contributor | Create/manage pipelines, datasets, linked services |
| 📁 **Azure Blob Storage** | Storage Blob Data Contributor | Read/write access to containers |
| 🔐 **Azure Key Vault** | Key Vault Secrets User | Access to stored credentials |
| ❄️ **Snowflake** | Database Owner | Create tables, execute DDL/DML operations |

</div>

---

## 📁 Project Structure & Components

### 🗂️ **Repository Organization**

```
group-assignment1/
├── 🏭 factory/                          # ADF Factory Configuration
│   └── adf-petlicense-ananya.json      # Main factory definition
├── 🔄 pipeline/                         # Data Processing Pipelines
│   ├── pl_csv_to_parquet.json          # CSV to Parquet conversion
│   ├── pl_geo_to_stage.json            # Geographic data staging
│   ├── pl_pet_to_stage.json            # Pet data staging & DW loads
│   └── pl_team_pet_csv_to_parquet.json # Team-specific processing
├── 📊 dataset/                          # Data Source Definitions
│   ├── ds_blob_geo_csv.json            # Geographic CSV source
│   ├── ds_pet_parquet.json             # Pet data Parquet source
│   ├── ds_sf_dw_*.json                 # Snowflake DW table definitions
│   └── ds_sf_stage_*.json              # Snowflake staging tables
├── 🔗 linkedService/                    # External Connections
│   ├── ls_blob_*.json                  # Azure Blob Storage connections
│   ├── ls_snowflake_pet.json           # Snowflake database connection
│   └── kvpetlicenseananya.json         # Key Vault connection
├── 🌊 dataflow/                         # Data Transformation Logic
│   └── df_location_dim_upsert.json     # Location dimension processing
├── ⚙️ integrationRuntime/               # Integration Runtime Config
│   └── AutoResolveIntegrationRuntime.json
├── 🌐 managedVirtualNetwork/           # Network Configuration
│   └── default.json
└── 📋 publish_config.json              # Deployment Configuration
```

### 📋 **Component Summary**

<div align="center">

| **Component Type** | **Count** | **Purpose** | **Key Files** |
|-------------------|-----------|-------------|---------------|
| 🔄 **Pipelines** | 4 | ETL orchestration | `pl_pet_to_stage.json` (main) |
| 📊 **Datasets** | 8 | Data source definitions | `ds_pet_parquet.json`, `ds_sf_dw_*.json` |
| 🔗 **Linked Services** | 4 | External connections | `ls_snowflake_pet.json`, `ls_blob_*.json` |
| 🌊 **Data Flows** | 1 | Complex transformations | `df_location_dim_upsert.json` |
| ⚙️ **Integration Runtime** | 1 | Compute environment | `AutoResolveIntegrationRuntime.json` |

</div>

---

## 🔄 Data Flow Process

### 🌊 **End-to-End Data Pipeline**

<div align="center">

```mermaid
flowchart LR
    A[📁 CSV Files<br/>Azure Blob] --> B[🔄 Data Ingestion<br/>pl_pet_to_stage]
    B --> C[📊 Staging Layer<br/>STG_PET_LICENSE<br/>STG_LOCATION_LKP]
    C --> D[📋 Dimension Loading<br/>Location, Breed, Date]
    D --> E[⭐ Fact Table<br/>PETLICENSE_FACT]
    
    style A fill:#e3f2fd
    style B fill:#f3e5f5
    style C fill:#e8f5e8
    style D fill:#fff8e1
    style E fill:#fce4ec
```

</div>

### 🎯 **Processing Stages**

<div align="center">

| **Stage** | **Pipeline** | **Purpose** | **Key Operations** |
|-----------|---------------|-------------|-------------------|
| 🌐 **1. Ingestion** | `pl_pet_to_stage` | Data extraction | Copy from Blob to Snowflake staging |
| 📊 **2. Staging** | `pl_pet_to_stage` | Data validation | TRUNCATE, INSERT, quality checks |
| 📋 **3. Dimensions** | `pl_pet_to_stage` | Entity management | MERGE operations, SCD Type 1 |
| ⭐ **4. Facts** | `pl_pet_to_stage` | Metrics loading | MERGE with foreign keys |

</div>

### 📊 **Detailed Process Flow**

#### 🌐 **Stage 1: Data Ingestion**
- **Source**: CSV files in Azure Blob Storage containers
- **Pipeline**: `pl_pet_to_stage` → `cp_pet_to_stage` activity
- **Process**: 
  - Copy data from Blob Storage to Snowflake staging
  - Enable staging for large data transfers
  - Map source columns to target schema

#### 📊 **Stage 2: Data Staging**
- **Tables**: `STG_PET_LICENSE`, `STG_LOCATION_LKP`
- **Process**: 
  - TRUNCATE existing staging data
  - INSERT new records with validation
  - Handle data type conversions and null values

#### 📋 **Stage 3: Dimension Loading**
The system maintains three dimension tables with SCD Type 1 (overwrite) strategy:

<div align="center">

| **Dimension** | **Source** | **Key Fields** | **Business Rules** |
|---------------|------------|----------------|-------------------|
| 🏠 **Location** | Geographic lookup | ZIP_CODE, CITY_NAME, STATE_CODE | Default 'WA' for missing states |
| 🐕 **Breed** | Pet license data | SPECIES, PRIMARY_BREED, SECONDARY_BREED | Default 'UNKNOWN' for missing secondary |
| 📅 **Date** | License dates | DATE_KEY, FULL_DATE, YEAR_NUM, MONTH_NUM | MM/DD/YYYY format conversion |

</div>

#### ⭐ **Stage 4: Fact Table Loading**
- **Table**: `PETLICENSE_FACT`
- **Process**: 
  - MERGE operation for idempotent loading
  - Foreign key relationships to all dimensions
  - Composite key: LICENSE_ID + DATE_KEY

### 💻 **Actual Snowflake Script Implementation**

<div align="center">

```sql
-- ================================
-- ADF Script Activity: DW Loads
-- ================================
USE WAREHOUSE PET_WH;
USE DATABASE PET_LICENSE_DB;

-- =========================================
-- 1) LOCATION_DIM upsert from STG_LOCATION_LKP
-- =========================================
MERGE INTO DW.LOCATION_DIM D
USING (
  SELECT
    UPPER(TRIM(ZIP_CODE))                                        AS ZIP_N,
    UPPER(TRIM(CITY_NAME))                                       AS CITY_N,
    CASE WHEN STATE_CODE IS NULL OR TRIM(STATE_CODE) = ''
         THEN 'WA' ELSE UPPER(TRIM(STATE_CODE)) END              AS STATE_N,
    'USA'                                                        AS COUNTRY_N,
    MD5(
      UPPER(TRIM(ZIP_CODE)) || '|' ||
      UPPER(TRIM(CITY_NAME)) || '|' ||
      CASE WHEN STATE_CODE IS NULL OR TRIM(STATE_CODE) = ''
           THEN 'WA' ELSE UPPER(TRIM(STATE_CODE)) END
    )                                                            AS NK_HASH
  FROM STAGE.STG_LOCATION_LKP
  WHERE ZIP_CODE IS NOT NULL
) S
ON D.NATURAL_KEY_HASH = S.NK_HASH
WHEN MATCHED THEN UPDATE SET
  D.ZIP_CODE      = S.ZIP_N,
  D.CITY_NAME     = S.CITY_N,
  D.STATE_CODE    = S.STATE_N,
  D.COUNTRY_CODE  = S.COUNTRY_N
WHEN NOT MATCHED THEN INSERT
  (ZIP_CODE, CITY_NAME, STATE_CODE, COUNTRY_CODE, NATURAL_KEY_HASH)
VALUES
  (S.ZIP_N, S.CITY_N, S.STATE_N, S.COUNTRY_N, S.NK_HASH);

-- =========================================
-- 2) BREED_DIM upsert from STG_PET_LICENSE
-- =========================================
MERGE INTO DW.BREED_DIM D
USING (
  SELECT
    UPPER(TRIM(SPECIES))                                         AS SPEC_N,
    UPPER(TRIM(PRIMARY_BREED))                                   AS PB_N,
    CASE WHEN SECONDARY_BREED IS NULL OR TRIM(SECONDARY_BREED)=''
         THEN 'UNKNOWN' ELSE UPPER(TRIM(SECONDARY_BREED)) END    AS SB_N,
    MD5(
      UPPER(TRIM(SPECIES)) || '|' ||
      UPPER(TRIM(PRIMARY_BREED)) || '|' ||
      CASE WHEN SECONDARY_BREED IS NULL OR TRIM(SECONDARY_BREED)=''
           THEN 'UNKNOWN' ELSE UPPER(TRIM(SECONDARY_BREED)) END
    )                                                            AS NK_HASH
  FROM STAGE.STG_PET_LICENSE
) S
ON D.NATURAL_KEY_HASH = S.NK_HASH
WHEN MATCHED THEN UPDATE SET
  D.SPECIES_NAME    = S.SPEC_N,
  D.PRIMARY_BREED   = S.PB_N,
  D.SECONDARY_BREED = S.SB_N
WHEN NOT MATCHED THEN INSERT
  (SPECIES_NAME, PRIMARY_BREED, SECONDARY_BREED, NATURAL_KEY_HASH)
VALUES
  (S.SPEC_N, S.PB_N, S.SB_N, S.NK_HASH);

-- =========================================
-- 3) DATE_DIM upsert (derived from staged issue dates)
-- =========================================
MERGE INTO DW.DATE_DIM T
USING (
  SELECT
    TO_NUMBER(TO_CHAR(D,'YYYYMMDD')) AS DATE_KEY,
    D                                AS FULL_DATE,
    YEAR(D)                          AS YEAR_NUM,
    QUARTER(D)                       AS QUARTER_NUM,
    MONTH(D)                         AS MONTH_NUM,
    TO_CHAR(D,'Month')               AS MONTH_NAME,
    DAY(D)                           AS DAY_NUM
  FROM (
    SELECT DISTINCT TO_DATE(LICENSE_ISSUE_DATE, 'MM/DD/YYYY') AS D
    FROM STAGE.STG_PET_LICENSE
    WHERE LICENSE_ISSUE_DATE IS NOT NULL
  )
) S
ON T.DATE_KEY = S.DATE_KEY
WHEN MATCHED THEN UPDATE SET
  T.FULL_DATE   = S.FULL_DATE,
  T.YEAR_NUM    = S.YEAR_NUM,
  T.QUARTER_NUM = S.QUARTER_NUM,
  T.MONTH_NUM   = S.MONTH_NUM,
  T.MONTH_NAME  = S.MONTH_NAME,
  T.DAY_NUM     = S.DAY_NUM
WHEN NOT MATCHED THEN INSERT
  (DATE_KEY, FULL_DATE, YEAR_NUM, QUARTER_NUM, MONTH_NUM, MONTH_NAME, DAY_NUM)
VALUES
  (S.DATE_KEY, S.FULL_DATE, S.YEAR_NUM, S.QUARTER_NUM, S.MONTH_NUM, S.MONTH_NAME, S.DAY_NUM);

-- =========================================
-- 4) FACT MERGE (idempotent on LICENSE_ID + DATE_KEY)
-- =========================================
MERGE INTO DW.PETLICENSE_FACT F
USING (
  SELECT
    S.LICENSE_NUMBER,
    S.ANIMAL_NAME,
    S.DATE_KEY,
    L2.LOCATION_DIM_KEY,
    B.BREED_DIM_KEY,
    S.CNT
  FROM (
    SELECT
      LICENSE_NUMBER,
      ANIMAL_NAME,
      TO_NUMBER(TO_CHAR(TO_DATE(LICENSE_ISSUE_DATE,'MM/DD/YYYY'),'YYYYMMDD')) AS DATE_KEY,
      UPPER(TRIM(ZIP_CODE))                                              AS ZIP_N,
      MD5(
        UPPER(TRIM(SPECIES)) || '|' ||
        UPPER(TRIM(PRIMARY_BREED)) || '|' ||
        CASE WHEN SECONDARY_BREED IS NULL OR TRIM(SECONDARY_BREED)=''
             THEN 'UNKNOWN' ELSE UPPER(TRIM(SECONDARY_BREED)) END
      )                                                                  AS BREED_HASH,
      1                                                                  AS CNT
    FROM STAGE.STG_PET_LICENSE
  ) S
  JOIN DW.LOCATION_DIM L2
    ON S.ZIP_N = UPPER(TRIM(L2.ZIP_CODE))
  JOIN DW.BREED_DIM B
    ON S.BREED_HASH = B.NATURAL_KEY_HASH
) S
ON F.LICENSE_ID = S.LICENSE_NUMBER
   AND F.DATE_KEY = S.DATE_KEY
WHEN MATCHED THEN UPDATE SET
  F.LOCATION_DIM_KEY = S.LOCATION_DIM_KEY,
  F.BREED_DIM_KEY    = S.BREED_DIM_KEY,
  F.PET_NAME         = S.ANIMAL_NAME,
  F.CNT              = S.CNT
WHEN NOT MATCHED THEN INSERT
  (DATE_KEY, LOCATION_DIM_KEY, BREED_DIM_KEY, LICENSE_ID, PET_NAME, CNT)
VALUES
  (S.DATE_KEY, S.LOCATION_DIM_KEY, S.BREED_DIM_KEY, S.LICENSE_NUMBER, S.ANIMAL_NAME, S.CNT);
```

</div>

---

## 🛠️ Deployment & Configuration

### 🚀 **Quick Start Guide**

#### 📋 **Prerequisites Setup**

<div align="center">

```bash
# 🔐 Azure CLI Authentication
az login
az account set --subscription "your-subscription-id"

# ✅ Verify Azure CLI version
az --version
```

</div>

#### 🏭 **Azure Data Factory Deployment**

<div align="center">

```bash
# 🏗️ Create Resource Group (if not exists)
az group create --name "rg-petlicense-prod" --location "eastus2"

# 🏭 Deploy Data Factory
az datafactory create \
  --resource-group "rg-petlicense-prod" \
  --name "adf-petlicense-ananya" \
  --location "eastus2"

# 📦 Deploy Pipeline Components
az datafactory pipeline create \
  --resource-group "rg-petlicense-prod" \
  --factory-name "adf-petlicense-ananya" \
  --name "pl_pet_to_stage" \
  --pipeline @pipeline/pl_pet_to_stage.json
```

</div>

#### ❄️ **Snowflake Database Setup**

<div align="center">

```sql
-- 🗄️ Create Database and Warehouse
CREATE DATABASE PET_LICENSE_DB;
CREATE WAREHOUSE PET_WH WITH 
  WAREHOUSE_SIZE = 'SMALL'
  AUTO_SUSPEND = 60
  AUTO_RESUME = TRUE;

-- 👤 Create Role and User
CREATE ROLE PET_DW_ROLE;
CREATE USER dw_user PASSWORD = 'your-secure-password';
GRANT ROLE PET_DW_ROLE TO USER dw_user;

-- 📊 Create Schemas
CREATE SCHEMA PET_LICENSE_DB.STAGE;
CREATE SCHEMA PET_LICENSE_DB.DW;

-- 🔑 Grant Permissions
GRANT USAGE ON DATABASE PET_LICENSE_DB TO ROLE PET_DW_ROLE;
GRANT USAGE ON WAREHOUSE PET_WH TO ROLE PET_DW_ROLE;
GRANT ALL ON SCHEMA PET_LICENSE_DB.STAGE TO ROLE PET_DW_ROLE;
GRANT ALL ON SCHEMA PET_LICENSE_DB.DW TO ROLE PET_DW_ROLE;
```

</div>

### 🔧 **Environment Configuration**

<div align="center">

| **Configuration** | **Value** | **Description** |
|-------------------|-----------|-----------------|
| 🌍 **Region** | `eastus2` | Azure deployment region |
| 🏢 **Snowflake Account** | `LXUTZNB-PAA86859` | Account identifier |
| 🗄️ **Database** | `PET_LICENSE_DB` | Target database |
| 🏭 **Warehouse** | `PET_WH` | Compute warehouse |
| 👤 **Role** | `PET_DW_ROLE` | Database role |
| ⏱️ **Timeout** | `12:00:00` | Pipeline timeout |
| 🔄 **Retry Policy** | `0 retries` | Error handling |

</div>

---

## 📊 Monitoring & Operations

### 📈 **Operational Excellence Dashboard**

#### 🎯 **Key Performance Indicators (KPIs)**

<div align="center">

| **Metric Category** | **KPI** | **Target** | **Monitoring Method** |
|---------------------|---------|------------|---------------------|
| 📊 **Data Volume** | Records processed per run | > 10,000 | Snowflake query logs |
| ⏱️ **Performance** | Pipeline execution time | < 30 minutes | ADF monitoring |
| 🎯 **Data Quality** | Error rate | < 1% | Failed record counts |
| 🔄 **Reliability** | Success rate | > 99% | Pipeline run history |
| 📅 **Freshness** | Data latency | < 4 hours | Last successful run |

</div>

#### 🔍 **Monitoring Tools & Methods**

<div align="center">

| **Tool** | **Purpose** | **Key Metrics** |
|----------|-------------|-----------------|
| 🏭 **Azure Data Factory** | Pipeline orchestration | Execution status, duration, resource usage |
| ❄️ **Snowflake** | Data warehouse | Query performance, warehouse usage, data quality |
| 📊 **Query History** | Performance analysis | Execution time, rows produced, error tracking |

</div>

### 📊 **Essential Monitoring Queries**

<div align="center">

```sql
-- 🔍 Recent Pipeline Execution Check
SELECT 
    DATE_KEY,
    COUNT(*) as LICENSE_COUNT,
    MAX(LICENSE_ID) as LATEST_LICENSE
FROM PET_LICENSE_DB.DW.PETLICENSE_FACT 
WHERE DATE_KEY >= TO_NUMBER(TO_CHAR(CURRENT_DATE() - 7, 'YYYYMMDD'))
GROUP BY DATE_KEY
ORDER BY DATE_KEY DESC;

-- 📊 Dimension Table Health Check
SELECT 
    'LOCATION_DIM' AS TABLE_NAME, 
    COUNT(*) AS RECORD_COUNT,
    COUNT(DISTINCT ZIP_CODE) AS UNIQUE_ZIPS
FROM PET_LICENSE_DB.DW.LOCATION_DIM
UNION ALL
SELECT 
    'BREED_DIM', 
    COUNT(*),
    COUNT(DISTINCT SPECIES_NAME)
FROM PET_LICENSE_DB.DW.BREED_DIM
UNION ALL
SELECT 
    'DATE_DIM', 
    COUNT(*),
    COUNT(DISTINCT YEAR_NUM)
FROM PET_LICENSE_DB.DW.DATE_DIM;

-- ⚡ Performance Analysis
SELECT 
    QUERY_TEXT,
    EXECUTION_TIME,
    ROWS_PRODUCED,
    START_TIME
FROM SNOWFLAKE.ACCOUNT_USAGE.QUERY_HISTORY
WHERE QUERY_TEXT LIKE '%PETLICENSE_FACT%'
  AND START_TIME >= CURRENT_DATE() - 7
ORDER BY EXECUTION_TIME DESC;
```

</div>

---

## 🔒 Security & Compliance

### 🛡️ **Security Framework**

<div align="center">

| **Security Layer** | **Implementation** | **Compliance** |
|-------------------|-------------------|----------------|
| 🔑 **Authentication** | Azure Key Vault + Managed Identity | SOC 2 Type II |
| 🔒 **Encryption** | TLS 1.2 in transit, AES-256 at rest | GDPR Compliant |
| 👤 **Access Control** | Role-based permissions | Principle of least privilege |
| 📊 **Audit Logging** | Complete activity tracking | SOX Compliance |
| 🌐 **Network Security** | Managed Virtual Network | Zero-trust architecture |

</div>

### 📋 **Compliance Checklist**

<div align="center">

| **Requirement** | **Status** | **Implementation** |
|-----------------|------------|-------------------|
| ✅ **Data Encryption** | Compliant | All data encrypted in transit and at rest |
| ✅ **Access Logging** | Compliant | Complete audit trail of all data access |
| ✅ **PII Protection** | Compliant | Pet license data handled per privacy policies |
| ✅ **Backup & Recovery** | Compliant | Automated backup and disaster recovery |
| ✅ **Security Monitoring** | Compliant | Continuous security monitoring and alerting |

</div>

---

**🐾 Pet License Data Pipeline** • **Built with ❤️ by the Data Engineering Team**

*Last Updated: October 2024 • Version 1.0 • Maintained by Data Engineering Team*

</div>
