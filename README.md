Certainly! Here's a structured README file based on your setup.

---

# World Cup Database Project

This project sets up a PostgreSQL database for World Cup game data, including teams, game details, and goals scored. It includes scripts to create the database schema, import data from CSV files, and query the database to retrieve various insights. The project was developed as part of a FreeCodeCamp course.

## Project Structure

- **`worldcup.sql`**: SQL file to recreate the `worldcup` database schema and import sample data.
- **`insert_data.sh`**: Bash script to insert team and game data from a CSV file into the database.
- **`queries.sh`**: Bash script with various SQL queries for extracting insights from the database.

---

## Prerequisites

- **PostgreSQL 12.17** or later
- Bash terminal

Ensure you have PostgreSQL and set up appropriate permissions for the user `freecodecamp`.

---

## Database Schema

### Tables

1. **teams**
   - `team_id` (Integer, Primary Key): Unique identifier for each team.
   - `name` (Varchar): Name of the team.

2. **games**
   - `game_id` (Integer, Primary Key): Unique identifier for each game.
   - `year` (Integer): Year of the World Cup game.
   - `round` (Varchar): Game round (e.g., Eighth-Final, Quarter-Final).
   - `winner_id` (Integer, Foreign Key): ID of the winning team.
   - `opponent_id` (Integer, Foreign Key): ID of the opponent team.
   - `winner_goals` (Integer): Goals scored by the winning team.
   - `opponent_goals` (Integer): Goals scored by the opponent team.

### Relationships

- **games** table references **teams** table with `winner_id` and `opponent_id`.

---

## Usage

### 1. Database Setup

1. Run the following command to create and initialize the database:
   ```bash
   psql -U postgres -f worldcup.sql
   ```

2. Use `\c worldcup` to connect to the newly created `worldcup` database.

### 2. Data Insertion

The `insert_data.sh` script reads data from `games.csv` and populates the **teams** and **games** tables.

#### Running the script:

```bash
bash insert_data.sh
```

### 3. Queries

The `queries.sh` script contains multiple queries to retrieve insights from the database, such as:

- Total number of goals by winning teams.
- Teams that played in specific rounds.
- Average goals scored.

#### Running the script:

```bash
bash queries.sh
```

### Key Query Examples:

- List of unique teams who played in the 2014 'Eighth-Final' round:

  ```sql
  SELECT DISTINCT name FROM teams
  RIGHT JOIN games ON teams.team_id = games.winner_id OR teams.team_id = games.opponent_id
  WHERE year = 2014 AND round = 'Eighth-Final';
  ```

## Notes

- Make sure `worldcup.sql`, `insert_data.sh`, and `queries.sh` have execute permissions.
- `insert_data.sh` expects `games.csv` with columns `YEAR, ROUND, WINNER, OPPONENT, WINNER_GOALS, OPPONENT_GOALS`.

---

## License

This project is open-source and licensed under the MIT License. 

---
