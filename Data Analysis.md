# Data Analysis Project with RStudio Cloud & Supabase

## Overview
This is a **4-week project** where each student works independently but follows a **standardized project scheme**.  
- Environment: **RStudio Cloud**  
- Database: **Postgres (via Supabase)**  
- Visualization: **ggplot2**  

Each student will create their own dataset, document it, and analyze it with R.  
The structure is the same for everyone, but the **topic/idea is unique** to each student.  

---
## Use the same Database from your Data Tools final project. It had:
- **3 tables** in the database (in Supabase/Postgres)  
- **5 rows per table** minimum  
- **Clear relationships** (at least one `FOREIGN KEY`)  
- **Documentation** in `README.md` and a **data dictionary**   

---

## Week-by-Week Breakdown

### Week 1 – Database Setup
1. Use the same database you had from your data tools final project 

**Sample R connection code:**
```r
con <- dbConnect(
  RPostgres::Postgres(),
  host = "abc123.supabase.co",   # from Supabase Project Settings > Database
  port = 5432,
  dbname = "postgres",           # usually stays postgres
  user = "postgres",             # Supabase gives you this
  password = "your-real-password", 
  sslmode = "require"
)

dbListTables(con)
```
### Week 2 – Data Analysis in R
1. You will use Posit Cloud for R online <a>https://posit.cloud/</a>
2. Start a new project and install these packages(First time only- Installed only once):
```R
install.packages("DBI")
install.packages("RPostgres")
install.packages("dplyr")
install.packages("ggplot2")
```
3. Query the database from RStudio Cloud.
```r
df <- dbGetQuery(con, "SELECT * FROM books;")
head(df)
```
4. Perform basic analysis: summaries, filtering, grouping.

```r
library(dplyr)
df %>%
  group_by(author_id) %>%
  summarise(avg_pages = mean(pages))
```
5. Use ggplot2 to visualize at least 2 insights.

```r
library(ggplot2)
ggplot(df, aes(x=genre, fill=genre)) +
  geom_bar() +
  theme_minimal()
```
### Week 3 – GitHub Submission
1. Push your work from RStudio Cloud to GitHub:
- README.md
- data_dictionary.md
- analysis.R (your code)
- Submit a Pull Request to the lecturer’s repository.
- Include your Supabase connection setup and query samples.

### Deliverables

1. A README.md (project overview)
2. R code (analysis.R) with ggplot visuals
3. GitHub pull request link
   
