# Eoscala 1.5

> [!NOTE]
> You can download Eoscala data from [Confoederatio Datavault](https://datavault.confoederatio.org/s/2Kytdej7ABpw4rr). It can be viewed at https://dataview.confoederatio.org/.

## Abstract.

This is the testing and validation repository for **Eoscala**, a geospatial database on economic indicators and national accounts from 10000BC to 2025AD. Most of this work is achieved via proxy modelling. Figures and methods reports are prepared here, sorted by version.

For prior versions of Eoscala/Velkscala before 1.5/1.0, check the <ins>Releases</ins> tab.

## Data Structure.

Geospatial database of economic indicators from 10000BC-2025AD, at 5-arcmin resolution. Most rasters are WGS84 Equirectangular, 4320×2160, and split into 127 timesteps: 1000-year intervals from 10000BC to 1AD, 100-year intervals from 1AD-1700AD, at 10-year intervals from 1700AD to 1950AD, and at 1-year intervals from 1950AD-2025AD. Cells with <1 inhabitant are excluded from per capita calculations.

Since rasters are encoded as GeoPNG, `app.R` contains an R Shiny app able to decode GeoPNGs. For those without access to R Studio, you may also use the web viewer at [Confoederatio Dataview](https://dataview.confoederatio.org/).

 The encoding of each set of rasters is given in **Data Structure**. All monetary units are given in Fiscal Year 2000 International Dollars (FY$2000). LCU conversions are available in `national_accounts/`.

**Note.**

For socioeconomic researchers, the following open datasets may also prove valuable:

1. Stadestér (Cities, part of Velkscala) | [Projects (1.1)](https://projects.confoederatio.org/c/Stadester)
2. Velkscala (Demographics) | [Datavault (1.0)](https://datavault.confoederatio.org/s/44Pfgt7ya8wE77b)
3. Eoscala (Economics) | [Datavault (1.5)](https://datavault.confoederatio.org/s/2Kytdej7ABpw4rr)
4. Atlas (Polities) | [Datavault (0.6)](https://datavault.confoederatio.org/s/aBeY4JP4QGFjqRL)

⚠️ **Data Caveats.**

1. In certain cases we have chosen to preserve the statistical borders used by historians or statisticians in secondary/aggregate sources for academic purposes. Some borders may therefore be anachronistic.

### Data Structure.

Percentage data is normalised from 0-1.

- `admin_modern/` - Subadministrative divisions used in Eoscala 1.5/Velkscala 1.0 processing.
  - `geocodes.csv`: ISO3 geocodes table
  - `geocodes.png`: ISO3 raster
  - `hmd.png`: Special area codes used by the [Human Mortality Database (HMD)](https://www.mortality.org/).
  - `hmd_geocodes.csv`: HMD geocodes table
  - `iso2.png`: ISO2 raster used by the [World Inequality Database (WID)](https://wid.world/).
  - `iso2_geocodes.csv`: ISO2 geocodes table
  - `iso3_ilo_geocodes.csv`: ISO3 geocodes table used by [ILOSTAT](https://ilostat.ilo.org/).
- `GDP_nominal/` - GDP (Nominal), aggregate
- `GDP_nominal_pc/` - GDP (Nominal) per capita
- `GDP_PPP/` - GDP (PPP), aggregate
- `GDP_PPP_pc/` - GDP (PPP) per capita
- `gini/` - Economic inequality. This is a composite index of assessed wealth Gini (prior to 1800AD) and income Gini (after 1800AD), since wealth Gini after 1800AD is of limited utility due to changes in financial/legal structures.
- `labourforce/` - Economically active workforce, aggregate
  - `labourforce_f_<year>.png` - Female active labourforce
  - `labourforce_m_<year>.png` - Male active labourforce
  - `labourforce_t_<year>.png` - Total active labourforce
- `LFPR/` - Labourforce Participation Rate (LFPR). Determines share of working-age cohorts active in the workforce
  - `lfpr_f_<year>.png` - Female LFPR
  - `lfpr_m_<year>.png` - Male LFPR
- `national_accounts/` - Tabular modern national and subnational accounts from 1800AD onwards.
  - **Note.** To procedurally generate `national_accounts/` rasters, you will require the usage of both the `admin_modern.js` and `wealth_income_WID.js` classes; whose configs can be modified to suit your purposes. This assumes the usage of [Vercengen](https://confoederatio.org/Vercengen/).
  - `data/` - Raw data per ISO2 country in `.csv` form. Restricted to enumeration years.
  - `metadata/` - Metadata containing variable names by subdivision and cohort indicator.
- `professions/` - Share of employment by economic activity.
  - `percentage/` - Percentage data.  
    **Note.** Summing up percentages may result in figures >100% if including those `not_in_work`.
    - `agriculture_f/m/t_<year>.png` - % of Female/Male/Total Workforce in Agriculture
    - `manufacturing_f/m/t_<year>.png` - % of Female/Male/Total Workforce in Manufacturing
    - `services_f/m/t_<year>.png` - % of Female/Male/Total Workforce in Services.
    - `informal_labour_f/m/t_<year>.png` - % of Female/Male/Total Workforce in Informal Labour.
    - `not_in_work_f/m/t_<year>.png` - % of Female/Male/Total Workforce not in work.
  - `total/` - Aggregate workforce per economic activity.
    - `agriculture_f/m/t_<year>.png` - Total Female/Male/Total Workforce in Agriculture
    - `manufacturing_f/m/t_<year>.png` - Total Female/Male/Total Workforce in Manufacturing
    - `services_f/m/t_<year>.png` - Total Female/Male/Total Workforce in Services.
    - `informal_labour_f/m/t_<year>.png` - Total Female/Male/Total Workforce in Informal Labour.
    - `not_in_work_f/m/t_<year>.png` - Total Female/Male/Total Workforce not in work.
