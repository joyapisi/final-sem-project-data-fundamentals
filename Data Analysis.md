# Data Analysis Project with RStudio Cloud & Supabase

## Overview
This is a **4-week project** where each student works independently but follows a **standardized project scheme**.  
- Environment: **RStudio Cloud**  
- Database: **Postgres (via Supabase)**  
- Visualization: **ggplot2**  

Each student will create their own dataset, document it, and analyze it with R.  
The structure is the same for everyone, but the **topic/idea is unique** to each student.  

---

## Project Scheme
- **3 tables** in the database (in Supabase/Postgres)  
- **5 rows per table** minimum  
- **Clear relationships** (at least one `FOREIGN KEY`)  
- **Documentation** in `README.md` and a **data dictionary**  
- **Upload to GitHub** and submit a **Pull Request** to lecturer’s repo  

---

## Week-by-Week Breakdown

### Week 1 – Database Setup
1. Create a new **Supabase project** (Postgres database).  
2. Design **3 related tables** (5+ rows each).  
   - Example idea: *Books*, *Authors*, *Publishers*.  
3. Insert sample data manually or via SQL scripts.  
4. Connect RStudio Cloud to the database using `RPostgres`.

**Sample R connection code:**
```r
library(DBI)
con <- dbConnect(
  RPostgres::Postgres(),
  host = "your-supabase-host.supabase.co",
  port = 5432,
  dbname = "postgres",
  user = "your-username",
  password = "your-password",
  sslmode = "require"
)

dbListTables(con)
```
### Week 2 – Documentation
1. Write a README.md that explains:
- Your project idea
- Why you chose it
- The database schema (ERD optional)
2. Create a data dictionary (data_dictionary.md) with:
- Table name
- Column name, type, description, example values
Keep documentation simple and consistent.

### Week 3 – Data Analysis in R
Query the database from RStudio Cloud.
```r
df <- dbGetQuery(con, "SELECT * FROM books;")
head(df)
```
Perform basic analysis: summaries, filtering, grouping.

```r
library(dplyr)
df %>%
  group_by(author_id) %>%
  summarise(avg_pages = mean(pages))
```
Use ggplot2 to visualize at least 2 insights.

```r
library(ggplot2)
ggplot(df, aes(x=genre, fill=genre)) +
  geom_bar() +
  theme_minimal()
```
### Week 4 – GitHub Submission
1. Push your work from RStudio Cloud to GitHub:
- README.md
- data_dictionary.md
- analysis.R (your code)
- Submit a Pull Request to the lecturer’s repository.
- Include your Supabase connection setup and query samples.

### Deliverables

1. Supabase database with 3 tables, 5+ rows each

2. README.md (project overview)
3. Data dictionary file
4. R code (analysis.R) with ggplot visuals
5. GitHub pull request link
   
### Example Project Ideas
- Movie reviews database + analysis of ratings
- Small shop (products, customers, orders) + sales analysis
- Sports teams, players, matches + performance visualization
- Recipes, ingredients, chefs + cost analysis
