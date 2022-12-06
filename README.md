# DMDD_Ass3
# NBA Players stat


# Team Members: 

Vikrant Pawar (email: pawar.vik@northeastern.edu)
Swapnil Bhasgauri(email: bhasgauri.s@northeastern.edu)

# Project Description: 

This project aims to create a database containing player stats, information about their coaches,their teams and the stadiums. The database will include: 

- Players information such as age, position, team name
- Players stats like games played, games won, defensive score, points
- Stadium information
- Coach details
- Team description

We aspire to help the viewers and managing team to get a better view of players' record and their playing status.

## Scope: 
We have selected the 2020 stats which includes all the information about the matches played during this season.

## Plan of Action:
We have used 2 websites to scrape the data: 
-https://www.basketball-reference.com/
-https://en.hispanosnba.com/nba-arenas

### Website Scraping: 
As most of the details about the NBA games and players are available on the Basketball Reference’s website, we have scraped multiple pages to gather information in thei respective tables. We have used the other website to collect the stadium details of each team. We have used Python to scrape data.
We have collated all the above data sources to create a database and established connections between them to provide precise information for the same.



## Data Cleaning:


1. Players Table:

- Removed all the * marks from the fields using replace() in python
- Unwanted columns were removed  
 
2. Player_Stats Table:

- Removed all the * marks from the fields using replace() in python
- Unwanted columns were removed 

3. Team Table:

- Removed all the * marks from the fields using replace() in python
- Unwanted columns were removed 


4. Coach Table:

- Removed all the * marks from the fields using replace() in python
- Unwanted columns were removed 

5. Stadium Table:

- Removed all the * marks from the fields using replace() in python
- Unwanted columns were removed 


## Assignment Execution Steps:

Run the below Queries for the complete code Execution by following the given steps:


## 1. Create PLAYER table

	CREATE TABLE PLAYER(
        Player_Name VARCHAR(50),
        Position VARCHAR(50),
        Age VARCHAR(10),
        TEAM VARCHAR(50)
        );


## 2. Create TEAM table

	CREATE TABLE TEAM(
	Win Integer,
	Loss Integer,
	Win_Loss_Percent Integer,
	Points_Per_Game Decimal,
	Opponents_Points_Per_Game Decimal,
	SRS Decimal,
	Team_Name VARCHAR(50)
	);



## 3. Create PLAYER_STATS table

	CREATE TABLE PLAYER_STATS(
	Player VARCHAR(50),
	Game VARCHAR(50),
	Game_Started VARCHAR(50),
	Minutes_Played VARCHAR(50),
	Field_Goals VARCHAR(50),
	Field_Goal_Attempts VARCHAR(50) ,
	Field_Goal_Percentage VARCHAR(50),
	3_Points VARCHAR(50),
	3_Points_Attempts VARCHAR(50),
	3_Points_Percentage VARCHAR(50),
	2_Points VARCHAR(50),
	2_Points_Attemps VARCHAR(50),
	2_Points_Percentage VARCHAR(50),
	Effective_Field_Goal_Percentage VARCHAR(50),
	Free_Throws VARCHAR(50),
	Free_Throws_Attempts VARCHAR(50),
	Free_Throws_Percentage VARCHAR(50),
	Offensive_Rebounds VARCHAR(50),
	Defensive_Rebounds VARCHAR(50),
	Total_Rebounds VARCHAR(50),
	Assists VARCHAR(50),
	Steals VARCHAR(50),
	Blocks VARCHAR(50),
	Turnover VARCHAR(50),
	Personal_Fouls VARCHAR(50),
	Points VARCHAR(50)
	);



## 4. Create STADIUM Table

	CREATE TABLE STADIUM(
	TEAM VARCHAR(50),
	Stadium_Name VARCHAR(50),
	size VARCHAR(50)
	);



## 5. Create COACH table

	CREATE TABLE COACH(
	COACH_ID VARCHAR(50),
	TEAM_ID VARCHAR(50),
	Coach_Name VARCHAR(50),
	Games Integer,
	Win Integer,
	Loss Integer,
	Win_Percentage Decimal
	);



#### Add Foreign Key constraints

        ALTER TABLE PLAYER_STATS
	ADD CONSTRAINT PLAYER_STATS_fk  FOREIGN KEY (PLAYER_NAME)
	REFERENCES PLAYER(PLAYER_NAME);

	ALTER TABLE PLAYER
	ADD CONSTRAINT PLAYER_fk  FOREIGN KEY (TEAM_NAME)
	REFERENCES TEAM(TEAM_NAME)

	ALTER TABLE COACH
	ADD CONSTRAINT COACH_fk  FOREIGN KEY (TEAM_NAME)
	REFERENCES TEAM(TEAM_NAME)
 
	ALTER TABLE STADIUM
	ADD CONSTRAINT STADIUM_fk  FOREIGN KEY (TEAM_NAME)
	REFERENCES TEAM(TEAM_NAME)

## 6. Run the Python Script for scraping Basketball Websites in Jupyter Notebook

#### SQL to insert data in Coach Table

	INSERT INTO COACH VALUES(301,201,'Darvin Ham',11,2,9,0.182);
	INSERT INTO COACH VALUES(302,202,'Chauncey Billups',94,36,58,0.383);
	INSERT INTO COACH VALUES(303,203,'Jacque Vaughn',231,68,163,0.294);
	INSERT INTO COACH VALUES(304,204,'Steve Kerr',640,433,207,0.677);
	INSERT INTO COACH VALUES(305,205,'Erik Spoelstra',1125,665,460,0.591);
	INSERT INTO COACH VALUES(306,206,'Wes Unseld Jr.',94,41,53,0.436);
	INSERT INTO COACH VALUES(308,208,'Steve Clifford',650,295,355,0.454);
	INSERT INTO COACH VALUES(310,210,'Nate McMillan',1381,739,642,0.535);
	INSERT INTO COACH VALUES(311,211,'Stephen Silas',166,39,127,0.235);
	INSERT INTO COACH VALUES(312,212,'Billy Donovan',567,326,241,0.575);

## Use Cases
          

### 1. What are the effective field goal percentages of each team?	

SQL Statement: 

	SELECT SUM(PS.Effective_Field_Goal_Percentage), T.Team_Name, P.Player_Name
	FROM Player P
	JOIN Player_Stats PS ON Player = Player_Name
	JOIN Team T ON Team_Name = Team
	GROUP BY Effective_Field_Goal_Percentage, Team_Name


### 2. What are the average minutes played by a particular player ?

SQL Statement:

        SELECT PS.Minutes_Played, P.Player_Name
	FROM Player_Stats PS
	JOIN Player P ON Player = Player_Name

### 3. Which player has the highest defensive block for each team?

SQL Statement:
      
       SELECT P.Player_Name, MAX(PS.Blocks), T.Team_Name
       FROM Player P
       JOIN Player_Stats PS ON Player = Player_Name
       JOIN Team T ON Team_Name = Team
       GROUP BY Team_Name


### 4. Who are the players that should be chosen for increasing the chances of a team to win?

SQL Statement:

	SELECT PS.Points, P.Player_Name
 	FROM Player_Stats PS
	JOIN Player P ON PS.Player = P.Player_Name


### 5.  What is the percentage of offensive rebounds per game of a particular player ?

SQL Statement:

	SELECT  distinct P.Player_Name, (PS.Offensive_Rebounds/Total_Rebounds) AS OFFENSIVE_PERCENTAGE
	FROM Player_Stats PS
	JOIN Player P ON Player = Player_Name
	WHERE P.Player_Name = 'Kadeem Allen'


### 6.	Which player had the highest points from each team that had the highest win?

SQL Statement:

	SELECT MAX(Points), P.Player_Name,  T.Team_Name
	FROM Player P
	JOIN Player_Stats PS ON Player = Player_Name
	JOIN Team T ON Team_Name = Team
	WHERE (SELECT MAX(Win) FROM Team)
	GROUP BY Team_Name


### 7. Which players have the lowest free throw percentage for each team?

SQL Statement:

	SELECT MIN(Free_Throws_Percentage), P.Player_Name,  T.Team_Name
	FROM Player P
	JOIN Player_Stats PS ON Player = Player_Name
	JOIN Team T ON Team_Name = Team
	GROUP BY Team_Name



### 8. Which player has the most number of steals in a particular team?

SQL Statement:

	SELECT MAX(Steals), T.Team_Name
	FROM Player_Stats PS
	JOIN Player P ON Player = Player_Name
	JOIN Team T ON Team_Name = Team
	GROUP BY Team_Name



### 9.  Which player has the highest number of assists in a particular team?

SQL Statement:

	SELECT MAX(Assists), T.Team_Name
	FROM Player_Stats PS
	JOIN Player P ON Player = Player_Name
	JOIN Team T ON Team_Name = Team
	GROUP BY Team_Name

### 10.  What is the percentage of defensive rebounds per game of a particular player ?
  
SQL Statement:
                      
	SELECT  distinct P.Player_Name, (PS.Defensive_Rebounds/Total_Rebounds) AS OFFENSIVE_PERCENTAGE
	FROM Player_Stats PS
	JOIN Player P ON Player = Player_Name
	WHERE P.Player_Name = 'Kadeem Allen'




## Sample data from all tables

### Player table:
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/Player%20table.png)


### Coach Table:
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/Coach%20Table.png)


### Player_stats Table:
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/Player%20Stats%20table.png)


### Stadium Table:
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/Stadium%20Table.png)


### Team Table: 
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/Team%20Table.png)
