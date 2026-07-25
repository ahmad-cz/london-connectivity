[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/X8qC8wqs)
# DS105A (2025/2026) - ✍️ Mini Project 2

<!-- Optionally, add an illustrative banner image here to give your project a visual identity -->
<!-- ![](figures/an-illustrative-banner.png) -->

**Author:** [Ahmad Abdulaziz](https://github.com/ahmad-cz)

This project is part of the [LSE DS105A Autumn Term 2025/2026](https://lse-dsi.github.io/DS105/2025-2026/autumn-term/course-info.qmd) course and aims to answer the question: **"Where are the areas in London with poor transport connectivity?"** with data from the [TfL Journey Planner API](https://api.tfl.gov.uk) and the [ONS Postcode Directory](https://data.london.gov.uk/dataset/postcode-directory-for-london-exp5p/).

**The timeline of the project was quite short, so I decided to address it the following way**: I defined connectivity mainly by the duration of travel (along with the average speed of a journey, which is of course based on distance/duration), with the intention of creating an MSOA-level choropleth map for all 983 MSOAs in London similar to [TfL's own official time mapping measure of connectivity](https://content.tfl.gov.uk/connectivity-assessment-guide.pdf), and then based on this analysing more in-depth whether differences in travel times and journey speeds within boroughs could be based on deprivation levels by comparing the most deprived and least deprived area within each borough.

My answer to the question is: Areas of west, east and southeast Outer London have the worst connectivity to Central London. This is especially for the boroughs of Hillingdon, Havering, Bromley and Bexley. Also, in 8 of London's boroughs, including the 4 of the top 10 overall worst-connected boroughs, the most deprived areas within the borough have substantially worse connectivity to central London than the least deprived neighbourhoods. Check out the [REPORT.md](REPORT.md) to understand how I arrived at this conclusion.


## 📂 Repository Structure

If you decide to clone this project and try to replicate my analysis, you will eventually end up with the following structure:

```output
/
├── NB01-Data-Collection.ipynb
├── NB02-Data-Transformation.ipynb
├── NB03-Exploratory-Data-Analysis.ipynb
├── README.md
├── REPORT.md
├── .env # You will have to make this yourself
├── .gitignore
├── data/
│   ├── .gitkeep
│   ├── processed/
│   │   ├── least_deprived_processed.csv
│   │   ├── most_deprived_processed.csv
│   │   └── msoa_duration.csv
│   └── raw/
│       ├── 2011_MSOAs/ # Contains shapefiles for the choropleth map, downloaded externally but tracked by Git
│       ├── least_deprived_postcodes.csv
│       ├── Local_Authority_Districts_Names_and_Codes_UK.csv # This was downloaded externally but should be tracked by Git
│       ├── london_postcodes-ons-postcodes-directory-feb22.csv # You will have to download this yourself as not tracked by Git
│       ├── most_deprived_postcodes.csv
│       ├── sample_postcodes_durations.csv
│       └── sample_postcodes.csv
└── figures/
    ├── data_science_workflow_2025_vertical.png
    ├── london_travel_choropleth.png
    └── speedchart.png
```

## How to Run

1. Register for a TfL API key at [api-portal.tfl.gov.uk](https://api-portal.tfl.gov.uk/)

2. Clone this repository to your local machine

    ```bash
    git clone <github-repo-ssh-url>
    ```

3. Create a `.env` file in the root directory and add your TfL API key:

    ```text
    TFL_API_KEY=your_key_here
    ```

4. Install the additional Python packages if you haven't already:
    ```bash
    pip install pandas
    pip install dotenv
    pip install numpy
    pip install seaborn
    pip install matplotlib
    pip install geopandas
    ```

5. Download the [ONS Postcode Directory](https://data.london.gov.uk/dataset/postcode-directory-for-london-exp5p/) and save it to the `data/raw/` folder.

6. Run `NB01` to collect all the data used in this project. If running this in the future, change the CURRENTDATE variable at the top of the CSV file to a more up-to-date date (in the format YYYYMMDD), as TfL's Journey Planner API doesn't output historical journeys. This notebook will populate the `data/raw/` folder with the raw CSV data. This will be: a sample_postcodes CSV file containing the sampled rows from the London Postcode Directory (1 postcode for each MSOA), a sample_postcodes_durations CSV file containing the same CSV file except with the durations from each postcode to LSE recorded in its own row, and separate CSV files for the most deprived and least deprived areas in each borough and their corresponding postcode and journey (total duration and walking duration) information.

7. Run `NB02` to recreate the `data/processed/` data. This will create processed and "cleaned" CSV files that will be used in NB03's analysis. Borough names will be added to all 3 CSV files. The MSOA data is trimmed to only include the necessary data for NB03's analysis. The data for the most deprived and least deprived areas is also trimmed to only include the necessary data for NB03, plus haversine distances are calculated between each postcode and central London, along with the average speed of each journey. No changes to variables are needed in this notebook.

8. Browse `NB03` to see how I explored the data and generated the insights curated for the [REPORT.md](REPORT.md).

# 📟 Get in touch

If you like my work, get in touch with me on [LinkedIn](hwww.linkedin.com/in/ahmad-cz) or [GitHub](https://github.com/ahmad-cz).
