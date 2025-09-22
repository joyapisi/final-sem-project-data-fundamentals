# Data Fundamentals Project: Admin Roles & Security in Supabase

## Overview
This is a **4-week project** for the Data Tools unit.  
Students will work with **Supabase (Postgres)** to implement user roles, admin privileges, and basic security rules.  
The goal is to learn how to manage data access, enforce least privilege, and document the security setup.  

---

## Project Scheme
- **Supabase Postgres database** with at least 3 tables  
- **5 rows per table** minimum  
- **Admin and Regular User roles**  
- **Row Level Security (RLS)** enabled  
- **Policies** for different role actions (read, insert, update, delete)  
- Documentation of the setup in a `README.md`  
- GitHub submission via Pull Request  

---

## Week 1 – Database Setup
1. Create a new Supabase project.  
2. Design at least 3 related tables (5 rows each). Example:  
   - `users` (basic info, role column: admin / user)  
   - `projects` (created by users)  
   - `tasks` (linked to projects)  
3. Insert sample data into the tables.  
4. Enable **Row Level Security** (RLS) for all tables.  

---

## Week 2 – Roles & Policies
1. Define **Admin** and **User** roles.  
   - Admin: full access (read, insert, update, delete)  
   - User: restricted access (can only read and insert their own data)  
2. Write SQL policies in Supabase. Example:  

```sql
-- Example policy: Users can only see their own tasks
create policy "Users can view their own tasks"
on tasks
for select
using (auth.uid() = user_id);

-- Example policy: Admins can manage all tasks
create policy "Admins have full access to tasks"
on tasks
for all
using (exists (
  select 1 from users where id = auth.uid() and role = 'admin'
));
```
## Week 3 – Security Features
1. Explore **Supabase Auth** and set up email/password or magic link sign-ins.  
2. Ensure that only authenticated users can access the database.  
3. Create at least **one custom function** that requires admin privileges. Example:  

```sql
create or replace function delete_project(project_id uuid)
returns void
language sql
security definer
as $$
  delete from projects where id = project_id;
$$;
```
## Week 4 – GitHub Submission
1. Push your work to GitHub with:  
   - `README.md` (project description, roles, policies explained)  
   - `schema.sql` (table creation & policies)  
   - `security_notes.md` (short notes on your security setup)  
2. Submit a **Pull Request** to the lecturer’s repository.  

---

## Deliverables
- Supabase project with 3 tables (5+ rows each)  
- Admin and User roles implemented  
- Row Level Security (RLS) and policies applied  
- At least one custom admin-only function  
- Documentation in GitHub (`README.md`, 
