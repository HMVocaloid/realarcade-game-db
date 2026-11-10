# realarcade-game-db

# Relational Game Client Catalog & Integration Database

A Microsoft Access relational database designed to track game metadata, category classifications, release timelines, developer attributes, and client integration readiness (`HasRGP`).

## 📌 Project Objectives
- **Data Normalization:** Transition flat single-table data into a structured relational schema to eliminate duplicate string entries and data anomalies.
- **Dynamic Reporting:** Implement parameter-driven queries allowing partial string wildcard searches across categories, release years, and developer names.
- **User Input Safeguards:** Create custom data entry forms with bound lookup controls and referential integrity constraints.

## 🛠️ Tech Stack & Concepts
- **Database Engine:** Microsoft Access (`.accdb`)
- **Language:** SQL
- **Concepts:** Normalization (1NF to 3NF), 1-to-Many Relationships, Foreign Keys, Referential Integrity, Parameterized Queries, Append/Update Queries.

## 🏗️ Database Architecture
The database connects game entries to developer entities via foreign key constraints:

- `Developers` ($1$) ─── ($\infty$) `Games`

### Key Schema Fields
- **Games Table:** `GameID` (PK), `GameName`, `CategoryID`, `ReleaseYear`, `DeveloperID` (FK), `HasRGP` (Boolean)
- **Developers Table:** `DeveloperID` (PK), `DeveloperName`

## 🔍 Featured Queries

### Multi-Criteria Parameter Search (`FindHasRGP`)
Allows users to filter game catalog records using flexible keyword matching:

```sql
SELECT Games.GameName, Games.Category, Games.ReleaseYear, Developers.DeveloperName, Games.HasRGP
FROM Developers INNER JOIN Games ON Developers.DeveloperID = Games.DeveloperID
WHERE (((Games.Category) Like "*" & [Enter game category] & "*") 
  AND ((Games.ReleaseYear) Like "*" & [Enter Game Year] & "*") 
  AND ((Developers.DeveloperName) Like "*" & [Enter developer] & "*"));
