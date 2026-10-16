Personal Spending Assistant

Project Overview:
This project is a personal finance assistant designed to help users understand and analyse their spending. It will use Python to process financial transaction data and provide useful summaries of spending habits.

Planned Features:
Upload financial transaction data from a CSV file.
Calculate total spending.
Summarise spending by category.
Identify the category with the highest spending.
Answer questions about the financial data using the Gemini API.
Display an interactive interface using Gradio.
Handle invalid inputs and test the program.

Technologies:
Python, Pandas, Google Gemini API, Gradio & Google Colab

Sample Input:
The assistant uses a CSV file containing transaction information with three columns: Description, Category and Amount.
Example:
Description:             Category:            Amount:
Supermarket              Groceries              60
Bus card                 Transport              20
Food shop                Groceries              40
Cinema                   Entertainment          30

Sample Output:
Using the example transactions above, the assistant should calculate:
Total spending: $150
Groceries: $100
Transport: $20
Entertainment: $30
Highest-spending category: Groceries — $100
