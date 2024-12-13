# FITWELL

# Project Overview
This project, titled FitWell, integrates a user authentication system and a BMI calculator application. The primary objectives are:

To provide a secure sign-up and login system using a MySQL database.
To allow users to calculate, view, and update their BMI (Body Mass Index) while storing this data for future reference.
To align with the Sustainable Development Goal (SDG) of "Good Health and Well-being," promoting health awareness through BMI tracking.
# Explanation of How Python Concepts, Libraries, etc., Were Applied
GUI Design:
The user interface is implemented with Tkinter and enhanced with CustomTkinter for a modern appearance.

Login and Signup windows are designed with placeholders and buttons to improve user experience.
The BMI calculator interface uses labels, entry fields, and dropdown menus to simplify data input.
Database Integration:

MySQL Connector handles the connection to a MySQL database for storing user credentials and BMI records.
SQL commands are used for CRUD operations, including user authentication, BMI record insertion, updates, and deletions.
File Handling:

The subprocess library is utilized to run the BMI calculator script (three.py) after successful login or signup.
Image Handling:

Pillow (PIL) is used to load and display images in the application interface.
Error Handling:

Exception handling mechanisms ensure robustness against invalid user inputs and database connection issues.
# Details of the Chosen SDG and Its Integration into the Project
The project aligns with SDG 3: Good Health and Well-being, which aims to ensure healthy lives and promote well-being for all ages. By allowing users to compute their BMI and track their weight and height, FitWell contributes to raising awareness about healthy body metrics. It provides actionable feedback on underweight, normal weight, overweight, and obesity categories, encouraging users to maintain a healthier lifestyle.
# Instructions for Running the Program
Setup:

Install Python (v3.8 or higher).
Install the required libraries using pip install tkinter mysql-connector-python pillow customtkinter.
Database Configuration:

Set up a MySQL database with the following credentials:
Host: localhost
User: root
Database: hidb for login/signup and bmidb for BMI records.
Create tables using the SQL commands included in the script.
Image File:

Place an image file named Fitwell.png in the script's directory or update the image_path variable to its location.
Running the Program:

Run the main script to start the login window. Use the command:
bash
Copy code
python <script_name>.py
Sign up or log in using valid credentials. After successful login/signup, the BMI calculator will launch.
Features Usage:

BMI Calculator: Input your name, weight, and height (with appropriate units) and press "Calculate BMI."
View Records: View saved BMI data through the "View Records" button.
Update/Delete Records: Modify or clear BMI records directly from the records window.
Logout: Exit the BMI calculator and return to the login interface.
Closing the Application:

Ensure all windows are closed, and the database connection is terminated.

