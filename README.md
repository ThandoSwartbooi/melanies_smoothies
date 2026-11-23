Smoothie Order App: Streamlit in Snowflake

A data application built with Streamlit in Snowflake, Python and SQL. Customers pick their fruits, name their smoothie order, and submit it. Everything is stored and read directly in Snowflake.

Built as part of the Snowflake Hands-On Essentials: Data Application Builders Workshop (Badge 3), with the lab work validated by Snowflake's automated grader, DORA.

Overview

The app is a custom smoothie order form for a fictional smoothie shop. The list of available fruits is not hard-coded. It is loaded from a Snowflake table, so the menu can change without touching the app code.

Features
Fruit menu loaded live from a Snowflake table (FRUIT_OPTIONS)
Multi-select ingredient picker, limited to a maximum of 5 fruits per order
Name field for the order
Orders saved to Snowflake when submitted
Nutrition information for chosen fruits from an external REST API
Technologies Used
Area	Tools
Application	Streamlit in Snowflake
Language	Python
Data access	Snowpark
Database	Snowflake (SQL)
Data loading	Internal stage, file format, COPY INTO
Version control	Git and GitHub
Database Setup

The app runs in the SMOOTHIES.PUBLIC schema, owned by the SYSADMIN role.

sql
USE ROLE SYSADMIN;

CREATE DATABASE IF NOT EXISTS SMOOTHIES;

CREATE TABLE SMOOTHIES.PUBLIC.FRUIT_OPTIONS (
    FRUIT_ID   NUMBER,
    FRUIT_NAME VARCHAR(25)
);

CREATE FILE FORMAT SMOOTHIES.PUBLIC.TWO_HEADERROW_PCT_DELIM
    TYPE = CSV,
    SKIP_HEADER = 2,
    FIELD_DELIMITER = '%',
    TRIM_SPACE = TRUE;

CREATE STAGE SMOOTHIES.PUBLIC.MY_UPLOADED_FILES
    DIRECTORY = (ENABLE = TRUE);

The fruit file is uploaded to the internal stage and loaded with the columns reordered during the load:

sql
COPY INTO SMOOTHIES.PUBLIC.FRUIT_OPTIONS
FROM (
    SELECT $2 AS FRUIT_ID, $1 AS FRUIT_NAME
    FROM @SMOOTHIES.PUBLIC.MY_UPLOADED_FILES/fruits_available_for_smoothies.txt
)
FILE_FORMAT = (FORMAT_NAME = SMOOTHIES.PUBLIC.TWO_HEADERROW_PCT_DELIM)
ON_ERROR = ABORT_STATEMENT
PURGE = TRUE;
How to Run
Run the SQL setup scripts in a Snowflake worksheet as SYSADMIN.
In Snowsight, go to Projects > Streamlit and create a Streamlit app in SMOOTHIES.PUBLIC.
Replace the default code with the contents of streamlit_app.py.
Click Run to preview, then Deploy.

No credentials are stored in this repository. The app uses the Snowflake session it is deployed in.

Project Structure
.
├── README.md
├── streamlit_app.py      # Streamlit in Snowflake application
├── sql/                  # Database setup and data loading scripts
└── screenshots/          # App and results screenshots
What I Learned
Building and deploying an application with Streamlit in Snowflake
Reading Snowflake tables into an app with Snowpark
Creating internal stages and file formats, and querying staged files before loading them
Reordering columns during COPY INTO using a SELECT on the staged file
Debugging data issues, including a trailing-space problem that caused a grading check to fail, and an SSL certificate problem with an external API
Keeping a clean repository and documenting a project for other people to read
Author

Thando Swartbooi ICT student at Sol Plaatje University, focused on Data Engineering, AI and Cloud Computing.
