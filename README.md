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
          

### 1. Which players are playing for the team with the highest srs?

SQL Statement:
	SELECT Player_Name, MAX(SRS)
	FROM Player p
	JOIN Team  ON Team_Name = TEAM
	GROUP BY Team_Name;
	
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_1.png)



### 2. Which player has the highest field goal percentage for a season and represents which team?

SQL Statement:
	SELECT PLayer, MAX(Effective_Field_Goal_Percentage), Team_Name
	FROM Player_Stats 
	JOIN Player ON Player = Player_Name
	JOIN Team  ON Team_Name = Team
	
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_2.png)

	


### 3. Which players have the 3 pointer percentage greater than 0.4 and which team they belong to?

SQL Statement:
	SELECT PLayer, 3_Points_Percentage, Team_Name
	FROM Player_Stats 
	JOIN Player ON Player = Player_Name
	JOIN Team  ON Team_Name = Team
	WHERE 3_Points_Percentage > 0.4;
	
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_3.png)



### 4. Which team has players of age group 25 to 30 and what are their particular points?

SQL Statement:
	SELECT PLayer, Age, Team_Name
	FROM Player_Stats 
	JOIN Player ON Player = Player_Name
	JOIN Team  ON Team_Name = Team
	WHERE Age between 25 AND 30;
	
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_4.png)



### 5.  Which all players are playing at centre position for the team?

SQL Statement:
	SELECT PLayer, position, Team_Name
	FROM Player_Stats 
	JOIN Player ON Player = Player_Name
	JOIN Team  ON Team_Name = Team
	WHERE position = 'C' 
	
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_5.png)



### 6.	Which player has the highest minutes played and for which team?

SQL Statement:
	SELECT PLayer, Team_Name, MAX(Minutes_Played)
	FROM Player_Stats 
	JOIN Player ON Player = Player_Name
	JOIN Team  ON Team_Name = Team
	
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_6.png)



### 7. Which all players are playing at power forward position for the team with highest srs?

SQL Statement:
	SELECT DISTINCT(PLayer), Team_Name, MAX(SRS) 
	FROM Player_Stats 
	JOIN Player ON Player = Player_Name
	JOIN Team  ON Team_Name = Team
	WHERE position = 'PF' ; 
	
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_7.png)




### 8. Which is the youngest player who has played the most games?

SQL Statement:
	SELECT DISTINCT(PLayer), MIN(Age), MAX(Game)
	FROM Player_Stats 
	JOIN Player ON Player = Player_Name
	JOIN Team  ON Team_Name = Team;
	
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_8.png)




### 9.  Which all teams have srs greater than 3 and who all are playing under them?
 
SQL Statement:
	SELECT DISTINCT(PLayer),SRS
	FROM Player_Stats 
	JOIN Player ON Player = Player_Name
	JOIN Team  ON Team_Name = Team
	WHERE SRS > 3;

![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_9.png)



### 10.  Which player has the highest points from each team?

SQL Statement:
	SELECT DISTINCT(PLayer),MAX(Points), Team
	FROM Player_Stats 
	JOIN Player ON Player = Player_Name
	JOIN Team  ON Team_Name = Team
	GROUP BY Team
	
	
![image](https://github.com/vikpawar22/DMDD_Ass3/blob/master/Images/UC_10.png)




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
