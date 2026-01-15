# GROUP PROJECT 4: International Student & Visa Management System (SQL Project)

## Project Overview
Managing visa applications, financial aid, and course enrollment for international students is often inefficient when done manually or across disconnected systems. This project creates a **centralized SQL database** to manage international students, dependents, tourist visas, and related information efficiently.  

The database models three types of visas (F-1, IR2, B-2), tracks students’ enrollment, financial aid, and employment at the university, while ensuring data consistency and operational efficiency. It is designed to help administrative staff, international student advisors, USCIS, SEVIS, and other stakeholders streamline processes, improve data accuracy, and support data-driven decision-making.

---

## Motivations & Benefits

### Motivations:
- **Streamline Processes:** Automate visa applications, financial aid disbursement, and course registration.  
- **Improve Data Accuracy:** Reduce manual entry errors and maintain consistent records.  

### Benefits:
- **Operational Efficiency:** Faster processing and reduced administrative burden.  
- **Data-Driven Insights:** Support decisions about international student recruitment, course planning, and visa compliance.  

---

## Users
- International Student Advisors  
- Financial Aid Officers  
- University Administration  
- USCIS (U.S. Citizenship and Immigration Services)  
- SEVIS (Student and Exchange Visitor Information System)  

---

## Business Rules
1. **Financial Aid Management:**  
   - Each financial aid record (Scholarship, Loan, Sponsor) is linked to a specific student.  
   - Types of aid include CGPA-based scholarships, loans with grace periods, and sponsors.  

2. **Student & Visa Management:**  
   - Each student must be linked to a valid visa.  
   - Track visa expiration, personal data, and dependent relationships.  

3. **Course Enrollment & Management:**  
   - Each course has sections distinguished by semester and year.  
   - Students can enroll in multiple sections; each enrollment is uniquely tracked.  

4. **Employment Tracking:**  
   - Students employed at the university are tracked by department, position, start, and end dates.  

5. **Tourist Visa Handling:**  
   - Track tourist visa holders individually, including length of stay and intended arrival date.  

---

## User Requirements
- **Comprehensive Data Access:** Students and administrative staff have role-based access to relevant data.  
- **Security & Privacy:** Sensitive information is protected using role-based access controls.  
- **Reporting & Analytics:** Generate reports on enrollment, employment, visa status, and financial aid.  
- **Notifications & Alerts:** System provides alerts for enrollment deadlines, visa expirations, and compliance issues.  
- **Maintenance & Support:** The system supports updates, issue resolution, and compliance adjustments.  

---

## Database Structure
The database consists of the following tables:

- **Visa:** Stores visa and personal details of students and tourists.  
- **Tourist:** Holds tourist visa details like stay duration and intended arrival date.  
- **Dependant:** Links dependents to primary visa holders.  
- **Student:** Tracks student records and visa expiration.  
- **Course:** Stores course details.  
- **Section:** Manages course sections by semester and year.  
- **Enrollment:** Tracks student enrollments in sections.  
- **FinancialAid:** Generic table linking financial aid to students.  
- **Scholarship, Loan, Sponsor:** Specific financial aid types.  
- **Employment:** Tracks student employment within the university.  

---

## Project Files
- `create_tables.sql` → Create all database tables and relationships.  
- `insert_data.sql` → Insert sample data for visas, students, courses, enrollment, financial aid, and employment.  
- `queries.sql` → Contains example SQL queries demonstrating:
  - Projection, arithmetic, aliasing, concatenation
  - WHERE clause, logical & comparison operators
  - Date functions, IN & subqueries
  - LIKE operator, aggregation, GROUP BY & HAVING
  - Conditional expressions, UNION, MINUS, INTERSECT
  - JOIN examples for relational queries

---

## Sample Queries

**1. Projection & Arithmetic**
```sql
SELECT Passport_ID, Visa_Type, First_Name, Last_Name, (Phone_Number / 2) AS Half_Phone_Number
FROM Visa;
```

**2. Join with Alias**
```sql
SELECT v.Passport_ID AS ID, v.First_Name || ' ' || v.Last_Name AS Full_Name,
       t.Duration_Of_Stay AS Stay_Duration, t.Intended_Arrival_Date AS Arrival_Date
FROM Visa v
JOIN Tourist t ON v.Passport_ID = t.Passport_ID;
```

**3.Aggregation & Group By**
```sql
SELECT Section.Course_ID, Course.Course_Name, COUNT(Enrollment.Student_ID) AS Total_Students
FROM Section
JOIN Enrollment ON Section.Section_ID = Enrollment.Section_ID
JOIN Course ON Section.Course_ID = Course.Course_ID
GROUP BY Section.Course_ID, Course.Course_Name;
```

**4.Conditional Expression**
```sql
SELECT Passport_ID, First_Name, Last_Name,
       CASE
           WHEN Visa_Type = 'F-1' THEN 'Student Visa'
           WHEN Visa_Type = 'B-2' THEN 'Tourist Visa'
           ELSE 'Other'
       END AS Visa_Category
FROM Visa;

```

## Technologies Used
- SQL (Structured Query Language)
- Any relational database system (MySQL, SQL Server, PostgreSQL, etc.)



