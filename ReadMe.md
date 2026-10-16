Personal Spending Assistant

Project Overview:
This project is a personal finance assistant designed to help users understand and analyse their spending. It will use Python to process financial transaction data and provide useful summaries of spending habits.

Planned Features:
1. Upload financial transaction data from a CSV file.
2. Calculate total spending.
3. Summarise spending by category.
4. Identify the category with the highest spending.
5. Answer questions about the financial data using the Gemini API.
6. Display an interactive interface using Gradio.
7. Handle invalid inputs and test the program.

Technologies:
1. Python
2. Pandas
3. Google Gemini API
4. Gradio
5. Google Colab

Sample Input:
The assistant uses a CSV file containing transaction information with three columns: Description, Category and Amount.
Example:
Descriptions: Supermarket, Bus card, Food shop and Cinema

Category: Groceries, Transport, Groceries and Entertainment 

Amount: $60, $20, $40 and $30

Sample Output:
Using the example transactions above, the assistant should calculate:

Total spending: $150

Groceries: $100

Transport: $20

Entertainment: $30

Highest-spending category: Groceries — $100



How to Run the Project
1. Open the notebook in Google Colab.
2. Add your Gemini API key to Google Colab Secrets using the name GEMINI_API_KEY.
3. Run the notebook cells in order, starting from the top.
4. Upload a CSV file containing the columns Description, Category and Amount.
5. Enter a question about your spending.
6. Read the response provided by the Personal Spending Assistant.
