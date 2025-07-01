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
- Merging production and inspection datasets
- Creating conditional quality outputs
- Error handling and exception transformation

---

## 🧠 Case study: Data transformation on steel coil manufacturing process raw data
1. Source data loading
-         = Csv.Document(File.Contents("C:\Users\SSASIKIR\OneDrive - Capgemini\Desktop\2025\Personal files\Office related\Data analysis\My sample projects\Inventory_dataset.csv"),[Delimiter=",", Columns=54, Encoding=1252, QuoteStyle=QuoteStyle.None])
2. Remove unnecessary top rows
-         = Table.Skip(Source,1)
3. 
