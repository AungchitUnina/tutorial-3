# Global-Scale Chlorophyll-a Monitoring in Inland Lakes for Water Quality Assessment Based on Remote Sensing and Machine Learning Models        
-----------------------------------------------------------------------------------------------------------------------------
**Aung Chit Moe** a,b*; **Khim Cathleen Saddi** a,b,c; **Ruodan Zhuang** a; **Domenico Miglino** a; **Jorge Saavedra Navarro** a; **Salvatore Manfreda** a  

a Department of Civil, Building and Environmental Engineering (DICEA), University of Naples Federico II, Naples, Italy  
b IUSS University School for Advanced Studies of Pavia, Pavia, Italy  
c Department of Civil Engineering and Architecture, Ateneo de Naga University, Naga, Philippines  

\* Corresponding author: **aungchit.moe@unina.it**

-----------------------------------------------------------------------------------------------------------------------------
## Data Sources 
-----------------------------------------------------------------------------------------------------------------------------
### 1 Gathered and Filtered Data
 #### a. Gathered Raw Insitu Data 
      Information of coordinates, Date, Lat, Long, Smapling Depth, Chla values, and Sources
 #### b. Filtered Raw Insitu Data 
      Information of coordinates, Date, Lat, Long, Smapling Depth, Chla values, and Sources
-----------------------------------------------------------------------------------------------------------------------------
### 2. Matchups 
#### a. Original in-situ-Sentinel-2 matchups
      Information of coordinates, Date, Lat, Long, Smapling Depth, Chla values, Sources, and spectral bands + SCL classes
#### b. Filtered in-situ-Sentinel-2 matchups by SCL classes (only water)
      Information of coordinates, Date, Lat, Long, Smapling Depth, Chla values, Sources, and spectral bands + only water SCL class
#### c. Filtered in-situ-Sentinel-2 matchups by SCL classes (only water) with True/False flags after data cleaning
      Information of coordinates, Date, Lat, Long, Smapling Depth, Chla values, Sources, and spectral bands + True/False flags
#### d. Filtered in-situ-Sentinel-2 matchups by SCL classes (only water) with only True flag after data cleaning
      Information of coordinates, Date, Lat, Long, Smapling Depth, Chla values, Sources, and spectral bands + only True flag

     > Sentinel-2: https://www.esa.int/Applications/Observing_the_Earth/Copernicus/Sentinel-2
-----------------------------------------------------------------------------------------------------------------------------
### 3. Extracted Features

| Feature Type | Description | No. | Features |
|--------------|------------|-----------------|---------|
| a. Band Features (BF) | *Original spectral bands* | Totally 10 features | B2, B3, B4, B5, B6, B7, B8, B8A, B11, B12 |
| b. Index Features (IF) | *Derived indices* | Totally 20 features | B8-B4/B8+B4, B3-B8/B3+B8, B8-B11/B8+B11, B8-B12/B8+B12, B8-B11/B8+B12, B8-B12/B8+B11, B3-B11/B3+B11, B3-B12/B3+B12, B3-B11/B3+B12, B3-B12/B3+B11, B4-B3/B4+B3, B3+B4/B8+B11, B3+B4/B8+B12, 4×(B3-B11)-(0.25 ×B8+2.75×B11), 4×(B3-B12)-(0.25×B8+2.75×B12), 4×(B3-B11)-(0.25×B8+2.75×B12), 4×(B3-B12)-(0.25×B8+2.75×B11), B4/B8, B4/B2, B5-B4/B5+B4 (Details in Section 3.3.1) |
| c. Derived Features (DF) | *Derived via mathematical functions* | Totally 19,600 features | Including squaring, cubing, reciprocation, logarithmic transformation, absolute value, and standardization, combined with addition, subtraction, multiplication, and division (Details in Section 3.3.1) |
| d. Band Index Features (BIF) | *Bands + RF/Knee/VIF--> IF* | Totally 15 features | B2, B3, B4, B5, B6, B7, B8, B8A, B11, B12, B5-B4/B5+B4, B4-B3/B4+B3, B8-B12/B8+B11, B4/B2, B4/B8 |
| e. Band Derived Features (BDF) | *Bands + RF/Knee/VIF-->DF* | Totally 15 features | B2, B3, B4, B5, B6, B7, B8, B8A, B11, B12, StdB4-StdB5, 1/B6-1/B7, 1/8A-StdB2, Std B5/(B4)^3, (B5)^2-(B2)^2 |
| f. Composite Features (CF) | *Bands + RF/Knee/VIF-->IF+DF* | Totally 20 features | B2, B3, B4, B5, B6, B7, B8, B8A, B11, B12, B5-B4/B5+B4, B4-B3/B4+B3, B8-B12/B8+B11, B4/B2, B4/B8, StdB4-StdB5, 1/B6-1/B7, 1/8A-StdB2, Std B5/(B4)^3, (B5)^2-(B2)^2 |


> **Note:**  
> In CSV files, derived feature names are simplified as:  
> A = Band 1, B = Band 2, C = Band 3, D = Band 4, E = Band 5, F = Band 6, G = Band 7, H = Band 8, I = Band 8A, J = Band 11, K = Band 12
-----------------------------------------------------------------------------------------------------------------------------

### 4. Selected Features for model input

| Feature Type | Description | No. | Features |
|--------------|------------|-----------------|---------|
| a. Band Features (BF) | *Original spectral bands* | Totally 10 features | B2, B3, B4, B5, B6, B7, B8, B8A, B11, B12 |
| b. Index Features (IF) | *Derived indices* | Totally 5 features | B5-B4/B5+B4, B4-B3/B4+B3, B8-B12/B8+B11, B4/B2, B4/B8 |
| c. Derived Features (DF) | *Derived via mathematical functions* | Totally 5 features | StdB4-StdB5, 1/B6-1/B7, 1/8A-StdB2, Std B5/(B4)^3, (B5)^2-(B2)^2 |
| d. Band Index Features (BIF) | *Bands + RF/Knee/VIF--> IF* | Totally 6 features | B5-B4/B5+B4, B5, B8-B12/B8+B11, B4-B3/B4+B3, B4/B2, B4/B8 |
| e. Band Derived Features (BDF) | *Bands + RF/Knee/VIF-->DF* | Totally 7 features | StdB4-StdB5, Std B5/(B4)^3, (B5)^2-(B2)^2, 1/B6-1/B7, B6, B3, B11 |
| f. Composite Features (CF) | *Bands + RF/Knee/VIF-->IF+DF* | Totally 7 features | StdB4-StdB5, B4/B2, B8-B12/B8+B11, B4-B3/B4+B3, B4/B8, 1/B6-1/B7, B11 |

> **Note:**  
> In CSV files, derived feature names are simplified as:  
> A = Band 1, B = Band 2, C = Band 3, D = Band 4, E = Band 5, F = Band 6, G = Band 7, H = Band 8, I = Band 8A, J = Band 11, K = Band 12

-----------------------------------------------------------------------------------------------------------------------------
## SCL Classes

| Value | Description | Color |
|------:|------------|-------|
| 0 | No Data (Missing data) | `#000000` |
| 1 | Saturated or defective pixel | `#ff0000` |
| 2 | Topographic casted shadows (called "Dark features/Shadows" for data before 2022-01-25) | `#2f2f2f` |
| 3 | Cloud shadows | `#643200` |
| 4 | Vegetation | `#00a000` |
| 5 | Not-vegetated | `#ffe65a` |
| 6 | Water | `#0000ff` |
| 7 | Unclassified | `#808080` |
| 8 | Cloud medium probability | `#c0c0c0` |
| 9 | Cloud high probability | `#ffffff` |
| 10 | Thin cirrus | `#64c8ff` |
| 11 | Snow or ice | `#ff96ff` |

Source: https://custom-scripts.sentinel-hub.com/custom-scripts/sentinel-2/scene-classification/



-----------------------------------------------------------------------------------------------------------------------------
## Global in-situ data sources
- Relevant water quality databases include the Global Lakes Water Quality Database by Naderian et al. (2024) (https://github.com/roohollahnoori/AWQDFGL/)
- the Global Freshwater Quality Database (https://gemstat.org/data-gemstat/)
- the Water Quality Portal (WQP) for the United States (https://www.waterqualitydata.us/)
- the European Environmental Agency (EEA) Waterbase (https://www.eea.europa.eu/en/)
- the Open Government Portal of Canada (https://search.open.canada.ca/opendata/)
- the Heterogeneous Data Platform for Operational Modeling and Forecasting of Swiss (https://www.datalakes-eawag.ch/) 
-----------------------------------------------------------------------------------------------------------------------------
