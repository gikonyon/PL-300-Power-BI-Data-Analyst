# Domain 1: Prepare the Data & Ingestion Pipelines (PL-300)

> **Core Focus:** Connecting to web data sources, parsing nested JSON datasets, shaping tables via Power Query, and writing M code.

---

## 1. Ingesting Structured JSON from GitHub

When building reports from cloud repositories or APIs, Power BI allows direct connection to web endpoints via Power Query. For our project tracking **AI Infrastructure CapEx vs. Regional Labor Impacts**, we ingest `ai_market_data.json` directly from GitHub.

### Steps in Power BI Service / Desktop:
1. Select **Get Data** > **Web**.
2. Paste the **Raw URL** of your JSON file from your GitHub repository:
   `https://raw.githubusercontent.com/gikonyon/PL-300-Power-BI-Data-Analyst/main/datasets/ai_market_data.json`
3. Power Query automatically detects the JSON root record. Click through the record fields to isolate the `metrics` list and convert it into a standard data table.

---

## 2. Power Query M Code Ingestion Script

Below is the complete M code script used in the Power Query **Advanced Editor** to parse, expand, and enforce data types on the AI market and labor impact dataset:

```powerquery
let
    // Step 1: Connect to the GitHub Raw JSON web endpoint
    Source = Json.Document(Web.Contents("[https://raw.githubusercontent.com/gikonyon/PL-300-Power-BI-Data-Analyst/main/datasets/ai_market_data.json](https://raw.githubusercontent.com/gikonyon/PL-300-Power-BI-Data-Analyst/main/datasets/ai_market_data.json)")),
    
    // Step 2: Navigate to the nested 'metrics' list containing corporate records
    metrics_List = Source[metrics],
    
    // Step 3: Convert the extracted list into a base Power Query table
    #"Converted to Table" = Table.FromList(metrics_List, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    
    // Step 4: Expand record keys into individual columns
    #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted to Table", "Column1", 
        {"quarter", "company", "category", "capex_billions", "revenue_billions", "net_income_billions", "regional_labor_impact"}, 
        {"Quarter", "Company", "Category", "CapEx_Billions", "Revenue_Billions", "Net_Income_Billions", "Regional_Labor_Impact"}
    ),
    
    // Step 5: Enforce strict data types for financial calculations and text analysis
    #"Changed Type" = Table.TransformColumnTypes(#"Expanded Column1",{
        {"Quarter", type text}, 
        {"Company", type text}, 
        {"Category", type text}, 
        {"CapEx_Billions", Currency.Type}, 
        {"Revenue_Billions", Currency.Type}, 
        {"Net_Income_Billions", Currency.Type}, 
        {"Regional_Labor_Impact", type text}
    })
in
    #"Changed Type"
