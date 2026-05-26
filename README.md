# Mental Health of International Students — SQL Exploratory Analysis

[![DataCamp](https://img.shields.io/badge/Project-DataCamp-03EF62?logo=datacamp&logoColor=white)](https://www.datacamp.com)
[![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen)]()

## Project Overview

This project replicates and extends the findings of a peer-reviewed 2019 study conducted at a Japanese international university. The original study — approved by multiple ethical and regulatory boards — surveyed students to investigate whether studying abroad increases the risk of mental health difficulties.

Using **PostgreSQL**, I explored a dataset of 286 students to determine whether international students show higher risk of depression, and whether **length of stay** is a contributing factor — examining three validated psychological metrics.


## Key Question

> **Does studying abroad affect mental health, and does the length of stay make it worse?**


## Dataset

The dataset (`students.csv`) contains survey responses from domestic and international students, including:

| Field | Description |
|---|---|
| `inter_dom` | Student type: International (`Inter`) or Domestic (`Dom`) |
| `stay` | Length of stay in years |
| `todep` | Depression score — PHQ-9 test |
| `tosc` | Social connectedness score — SCS test |
| `toas` | Acculturative stress score — ASISS test |
| `japanese_cate` | Japanese language proficiency (Low / Average / High) |
| `english_cate` | English language proficiency (Low / Average / High) |
| `academic` | Academic level (Undergraduate / Graduate) |
| `age`, `gender`, `region` | Demographic variables |

---

## Tools & Skills Used

- **PostgreSQL** — querying, filtering, aggregation
- `COUNT`, `AVG`, `ROUND` — summary statistics
- `WHERE`, `GROUP BY`, `ORDER BY` — data segmentation
- Interpreting validated psychological instruments (PHQ-9, SCS, ASISS)

---

## Analysis & Findings

The core query segments international students by length of stay and computes average scores across all three mental health dimensions:

```sql
SELECT stay,
    COUNT(inter_dom)       AS count_int,
    ROUND(AVG(todep), 2)   AS average_phq,
    ROUND(AVG(tosc),  2)   AS average_scs,
    ROUND(AVG(toas),  2)   AS average_as
FROM students
WHERE inter_dom = 'Inter'
GROUP BY stay
ORDER BY stay DESC;
```

**Results summary:**

| Stay (years) | Students | Avg Depression (PHQ) | Avg Social Connectedness (SCS) | Avg Acculturative Stress (ASISS) |
|:---:|:---:|:---:|:---:|:---:|
| 10 | 1 | 13.00 | 32.00 | 50.00 |
| 8 | 1 | 10.00 | 44.00 | 65.00 |
| 4 | 14 | 8.57 | 33.93 | 87.71 |
| 3 | 46 | 9.09 | 37.13 | 78.00 |
| 2 | 39 | 8.28 | 37.08 | 77.67 |
| 1 | 95 | 7.48 | 38.11 | 72.80 |

### Key Takeaways

- **International students with longer stays tend to show higher depression scores**, consistent with the original study's findings.
- **Social connectedness scores remain relatively stable or decline** over longer stays, suggesting students may not fully integrate socially even with time.
- **Acculturative stress is notably higher among students who have stayed 3–4 years**, pointing to a mid-stay vulnerability window that warrants further investigation.
- The findings broadly support the original study's conclusion that **social connectedness and acculturative stress are predictive of depression** in international student populations.

---

## Repository Structure

```
├── notebook.ipynb       # Main analysis notebook (DataCamp Workspace)
├── students.csv         # Dataset (286 students, 50 features)
├── mentalhealth.jpg     # Project illustration
└── README.md            # Project documentation
```

---

## Data Source

Based on a real 2019 study published following approval by ethical and regulatory boards at a Japanese international university. The dataset captures PHQ-9 (depression), SCS (social connectedness), and ASISS (acculturative stress) scores alongside demographic and academic variables.

---

## 👤 Author

Built as part of the **DataCamp Data Analyst** learning track.  
Feel free to connect or reach out for collaboration.

---

## 📜 License

This project is for educational and portfolio purposes. The dataset is derived from a published academic study and is used under DataCamp's project terms.
