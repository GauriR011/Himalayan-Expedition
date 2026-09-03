# Himalayan Expedition Analysis

## Project Overview

This project analyzes data from the Himalayan Database, focusing specifically on the `members` table. The dataset contains records of participants who took part in expeditions to peaks in the Himalayan ranges in Nepal, covering expeditions from Summer 1905 to Spring 2019.

The analysis focuses on two key areas:

1. Understanding how a climber's age relates to their success, death, and injury rates.
2. Examining how success, death, and supplemental oxygen usage have changed over time across the five most climbed Himalayan peaks.

The analysis uses data wrangling and visualization techniques in R to identify patterns and trends in climbing outcomes.

---

## Dataset

The analysis uses the `members` dataset from the Himalayan Database, obtained through the TidyTuesday GitHub repository.

The dataset contains **21 columns** and records information about individual expedition participants, including their personal characteristics, expedition details, climbing outcomes, injuries, and survival.

Some of the key columns include:

| Feature Names | Feature Descriptions |
| --- | --- |
| `expedition_id` | Unique identifier for an expedition |
| `member_id` | Unique identifier for a climber |
| `peak_id` | Unique identifier for a peak |
| `peak_name` | Name of the peak |
| `year` | Year of the expedition |
| `season` | Season of the expedition |
| `sex` | Sex of the climber |
| `age` | Age of the climber |
| `citizenship` | Citizenship of the climber |
| `expedition_role` | Role of the climber in the expedition |
| `hired` | Whether the climber was hired |
| `highpoint_metres` | Highest point reached |
| `success` | Whether the climber successfully reached the expedition's goal |
| `solo` | Whether the climb was solo |
| `oxygen_used` | Whether supplemental oxygen was used |
| `died` | Whether the climber died |
| `death_cause` | Cause of death |
| `death_height_metres` | Height at which the death occurred |
| `injured` | Whether the climber was injured |
| `injury_type` | Type of injury |
| `injury_height_metres` | Height at which the injury occurred |

---

## Questions to Be Answered

### Question 1

**Does a climber's age influence their likelihood of success and survival, and how do these rates compare across different age groups?**

### Question 2

**How have success and death rates evolved over time for the five most climbed peaks, and how does the usage of supplemental oxygen compare across the peaks?**

This allows us to examine whether climbing outcomes have improved, declined, or remained relatively stable over time, while also comparing oxygen usage between the most frequently climbed peaks.

---

## Methodology

### Question 1: Age and Climbing Outcomes

First, records with missing age values were removed. Climbers were then divided into six age groups:

| `<20` | `20–29` | `30–39` | `40–49` | `50–59` | `60+` |
| --- | --- | --- | --- | --- | --- |

For each age group, we calculated the average:

- Success rate
- Death rate
- Injury rate

The resulting data was transformed into a long format so that the three metrics could be compared easily.

A **faceted bar chart** was used, with age groups on one axis and the corresponding rates on the other. Each metric was displayed in its own facet with independent scales, allowing relatively small death rates to remain visible alongside the larger success rates. Rates were displayed as percentages for easier interpretation.

<p align = "center">
  <img width="800" height="300" alt="image" src="https://github.com/user-attachments/assets/59b5adf0-326d-4ef3-97a6-b632e2151ffb" />
</p>

Because the number of observations varies substantially between age groups, particularly for the `<20` and `60+` groups, estimates for these smaller groups may be more variable.

### Question 2: Trends Across the Most Climbed Peaks

First, the five most climbed peaks were identified based on the number of records associated with each peak.

The analysis then focused on these five peaks and aggregated the data by **peak and year** to calculate annual:

- Success rates
- Death rates
- Oxygen usage rates

Data from **2019 was excluded** because only Spring 2019 data was available, making it an incomplete year for trend analysis.

The visualization used was a **faceted line chart**, with separate panels for each peak and metric. Raw annual fluctuations were shown alongside **LOESS-smoothed trend lines** to make the overall trends easier to identify.

The years were also divided into four historical eras:

- **Pioneer:** 1905–1970
- **Expansion:** 1971–1990
- **Commercial:** 1991–2010
- **Modern:** 2011–2019

The eras were highlighted in the background of the visualization to provide additional historical context. 

<p align = "center">
  <img width="1061" height="1002" alt="image" src="https://github.com/user-attachments/assets/016b4aa7-67a4-4474-b8e8-58959c8b03e5" />
</p>

---

## What Do We Infer?

### Findings from Question 1

The visualization shows a clear relationship between age and climbing outcomes:

- **Success rates decrease as age increases.** Climbers under 20 and those aged 20–29 have the highest success rates, while the 60+ group has the lowest.
- The **20–29 age group has the highest death rate**.
- Death rates generally decrease with age, although there is a slight increase in the 60+ group.
- The **50–59 age group has the highest injury rate**.
- There appears to be a trade-off between success and safety: younger climbers tend to have higher success rates but also higher death rates, while older climbers have lower success rates and generally lower death rates.
- Climbers aged 60+ have the lowest success rate but a lower death rate than the 20–29 and 30–39 groups.

One possible interpretation presented in the analysis is that younger climbers may take more risks or attempt more dangerous routes, while older climbers may be more cautious. However, this analysis identifies patterns and does not establish that age itself causes these outcomes. 

### Findings from Question 2

The five most climbed peaks identified in the analysis are:

1. **Everest**
2. **Cho Oyu**
3. **Manaslu**
4. **Dhaulagiri I**
5. **Ama Dablam**

The visualization reveals several important trends:

- **Death rates have generally declined over time.** Everest, Cho Oyu, and Manaslu show substantial decreases, reaching near-zero levels during the Commercial and Modern eras.
- **Ama Dablam has maintained near-zero death rates from the Expansion era onwards.**
- **Dhaulagiri I is an exception**, showing a slight increase in death rates in later years, although its levels remain below those observed during the earlier eras.
- **Success rates generally improved over time.** Everest, Cho Oyu, and Manaslu show strong upward trends.
- Dhaulagiri I and Ama Dablam show greater variability, with Dhaulagiri I showing a decline in success rate in later years.
- Overall, success rates are higher and death rates are lower in the Commercial and Modern eras compared with the Pioneer and Expansion eras.
  
### Supplemental Oxygen Usage

Oxygen usage differs considerably between peaks:

- **Everest, Cho Oyu, and Manaslu** have substantially higher oxygen usage.
- **Ama Dablam** has near-zero oxygen usage throughout the period analyzed.
- **Dhaulagiri I** shows a gradual increase in oxygen usage, particularly during the Modern era.

The report also highlights a relationship between altitude and oxygen usage. Everest, Cho Oyu, Manaslu, and Dhaulagiri I are all above 8,000 metres, while Ama Dablam is approximately 6,800 metres. This suggests a pattern where higher-altitude peaks tend to have greater supplemental oxygen usage. 

One notable data consideration is **2015 on Everest**. A major earthquake in Nepal caused an avalanche at Everest Base Camp, resulting in the cancellation of the climbing season. Consequently, the data shows an unusual drop to zero for success and oxygen usage in that year. This was excluded from the trend analysis to prevent the exceptional event from distorting the broader trend. 

---

## Conclusion

The analysis suggests that **age is associated with climbing outcomes**, with younger climbers generally experiencing higher success rates but also higher death rates, while older climbers tend to have lower success and death rates.

Across the five most climbed peaks, **death rates have generally declined and success rates have improved over time**, particularly for Everest, Cho Oyu, and Manaslu. Supplemental oxygen usage is also substantially higher on the higher-altitude peaks, highlighting the greater reliance on oxygen at extreme elevations.

Overall, the visualizations reveal clear patterns in how **age, time, peak, and oxygen usage relate to Himalayan expedition outcomes**.
