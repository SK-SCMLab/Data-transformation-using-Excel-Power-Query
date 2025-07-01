# 👾 Fundamental-Data-transformation-using-Excel-Power-Query
This repository contains a comprehensive Excel-based Power Query use case for transforming complex steel manufacturing production and inspection data. The dataset simulates real-world operations involving coil production, inspection reports, machine scheduling and surface finish outcomes

The goal is to clean, transform, and analyze this data using fundamental Power Query techniques

---

## 👃 Dataset description
The raw dataset includes 
- Coil production records with embedded headers
- Machine logs with time-delimited status updates
- Inspection quality outputs in wide format
- Column naming inconsistencies
- Nested and malformed entries requiring exception handling

--- 

## 🦷 Use case objectives 
Using **Excel Power Query**, we solve challenges in:
- Normalizing column headers
- Pivoting & Unpivoting inspection records
- Creating conditional quality outputs
- Error handling and exception transformation

---

## 🧠 Case study: Data transformation on steel coil manufacturing process raw data
1. Source data loading
-         = Csv.Document(File.Contents("C:\Users\SSASIKIR\OneDrive - Capgemini\Desktop\2025\Personal files\Office related\Data analysis\My sample projects\Inventory_dataset.csv"),[Delimiter=",", Columns=54, Encoding=1252, QuoteStyle=QuoteStyle.None])
2. Remove unnecessary top rows
-         = Table.Skip(Source,1)
3. Use first rows as headers
-         = Table.PromoteHeaders(#"Removed Top Rows", [PromoteAllScalars=true])
4. Remove the selected columns
-        = Table.RemoveColumns(#"Promoted Headers",{"All constraints", "KT_Finish", "KT_IsValueFinish", "SO_TAGGED_Category", "KT_FinishGroup", "VendorDescription", "Vendor", "QualityDecision"})
5. Reorder the required columns
-        = Table.ReorderColumns(#"Removed Columns1",{"BatchNo", "IsEligibleForCP", "StockingPoint", "WIP/FG", "ProductClass", "WIDTH", "THICK", "SegmentGroup", "UOM", "UnresQuantity", "UDDate", "SERIES", "QUALITY", "MaterialNo", "LENGTH", "InventoryType", "GradeCode", "BatchCreationDate", "GRADE", "EDGE_CON_CODE", "EDGE_CON", "PlantCode", "ProdOrdText", "AgingInDays", "SLB_GR_COND", "HEAT_NUMBER", "APL_WC", "DaysSpan", "Diameter", "HasProduct", "MICRO_JBS_010", "WorkCenter", "GradeGroupDesc", "HR_COIL_NO", "HasTemplateProductSpecification", "MICRO_JBS_040", "StorageLocation", "PPDS_Stock_Type", "PrevWorkCenter", "REMARKS", "QA_RemShortText", "SPD_BATCH_NO", "IsEligibleForOC", "HasOCInventory", "FINISH", "HasCPInventory"}
6. Remove the unwanted and unselected columns after reordering
-        = Table.SelectColumns(#"Reordered Columns",{"BatchNo", "IsEligibleForCP", "StockingPoint", "WIP/FG", "ProductClass", "WIDTH", "THICK", "SegmentGroup", "UOM", "UnresQuantity", "UDDate", "SERIES", "QUALITY", "MaterialNo", "LENGTH", "InventoryType", "GradeCode", "BatchCreationDate", "GRADE", "EDGE_CON_CODE", "EDGE_CON", "PlantCode"})
7. Change the Date format of the attribute Batch creation date
-        = Table.TransformColumnTypes(#"Changed Type",{{"BatchCreationDate", type date}})
8. Create a duplicate column for Batch creation and represent it in Quarters
-        = Table.TransformColumns(#"Renamed Columns",{{"Quarter", Date.QuarterOfYear, Int64.Type}})
9. Filter out the data rows having length ≠ 0
-        = Table.SelectRows(#"Removed Columns2", each ([LENGTH] <> "0"))
10. Remove blank rows for the attributes ProductState & PlantCode
-        = Table.SelectRows(#"Removed Blank Rows", each not List.IsEmpty(List.RemoveMatchingItems(Record.FieldValues(_), {"", null})))
11. Pivot the ProductState across the available plant codes
-        = Table.Pivot(#"Removed Blank Rows1", List.Distinct(#"Removed Blank Rows1"[ProductState]), "ProductState", "PlantCode", List.Count)
12. Extract the Stocking point Id from the string using the delimiter '_'
-        = Table.TransformColumns(#"Renamed Columns1", {{"StockingPoint", each Text.BeforeDelimiter(_, "_"), type text}})

---

## 🧑‍🦱 Excel functionalities used
- Power Query Editor

---

## 👀 Requirements
- Microsoft Excel 2016 or later
- Excel understanding

---

*"Data is the new oil" -Clive Humby*
