let
    // Step 1: Connect to the GitHub Raw URL endpoint
    Source = Json.Document(Web.Contents("https://raw.githubusercontent.com/gikonyon/PL-300-Power-BI-Data-Analyst/main/datasets/ai_market_data.json")),
    
    // Step 2: Navigate to the nested 'metrics' list
    metrics_List = Source[metrics],
    
    // Step 3: Convert List to Table
    #"Converted to Table" = Table.FromList(metrics_List, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    
    // Step 4: Expand record fields into structured columns
    #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted to Table", "Column1", 
        {"quarter", "company", "category", "capex_billions", "revenue_billions", "net_income_billions", "regional_labor_impact"}, 
        {"Quarter", "Company", "Category", "CapEx ($B)", "Revenue ($B)", "Net Income ($B)", "Regional Labor Impact"}
    ),
    
    // Step 5: Enforce Data Types
    #"Changed Type" = Table.TransformColumnTypes(#"Expanded Column1",{
        {"Quarter", type text}, 
        {"Company", type text}, 
        {"Category", type text}, 
        {"CapEx ($B)", Currency.Type}, 
        {"Revenue ($B)", Currency.Type}, 
        {"Net Income ($B)", Currency.Type}, 
        {"Regional Labor Impact", type text}
    })
in
    #"Changed Type"
