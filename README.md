Melanie's Smoothies
A Streamlit application built as part of the Snowflake Data Application Builders Workshop.

This application allows users to create custom smoothie orders, retrieve nutritional information for selected fruits, and store orders in a Snowflake database.

🚀 Features
Select up to 5 fruits for a custom smoothie
Retrieve fruit nutrition information via API
Store smoothie orders in Snowflake
Track customer names and ingredients
Use Snowpark to query Snowflake data
Deployed using Streamlit and managed through GitHub
🛠️ Technologies Used
Python
Streamlit
Snowflake
Snowpark
SQL
GitHub
📂 Project Structure
melanies_smoothies/
│
├── streamlit_app.py
├── requirements.txt
└── README.md
🧑‍💻 How It Works
The application retrieves available fruit options from Snowflake.
Users enter their name and select smoothie ingredients.
The application looks up fruit nutrition information using an external API.
The selected ingredients are stored in Snowflake.
Orders can be tracked and managed through Snowflake tables.
🗄️ Snowflake Objects Used
SMOOTHIES.PUBLIC.FRUIT_OPTIONS
SMOOTHIES.PUBLIC.ORDERS
📸 Project Highlights
During this project I:

Built a data application using Streamlit
Connected Streamlit to Snowflake
Worked with Snowpark DataFrames
Used GitHub for source control
Wrote SQL queries to manage and validate data
Completed the Snowflake Data Application Builders Workshop
🎓 Learning Outcomes
This project helped strengthen my skills in:

Python development
Data engineering fundamentals
Snowflake architecture
Database design
Git and version control
Application troubleshooting and debugging
⚠️ Note
This project was developed as part of a Snowflake hands-on workshop. Some external API functionality may depend on the availability of third-party services.

👤 Author
Thando Swartbooi

GitHub: https://github.com/ThandoSwartbooi

