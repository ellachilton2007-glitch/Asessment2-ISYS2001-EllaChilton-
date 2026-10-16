# Developer Diary
# Diary Entry 1: Understanding the Assessment – 29th September 2026
What I was trying to do: I wanted to understand the assessment requirements and plan what my Personal Spending Assistant needed to do before I started coding.

AI prompt: “I am creating a personal spending assistant for my programming assessment. What should the main objectives of my assistant be, and what features should I include to make it as effective and useful as possible? I want it to help users understand their spending, analyse transaction data and answer questions about their finances.”

Response: 
“I would recommend making the personal spending assistant simple to use, accurate and helpful for understanding spending habits. The main objectives should be:
•Analyse spending: Calculate total spending and show how much money is spent in each category.
•Identify spending patterns: Find the category where the user spends the most money.
•Read transaction data: Allow users to upload a CSV file containing their transactions.
•Answer questions: Use Gemini AI to answer questions about the user's spending based on their actual transaction data.
•Validate data: Check for missing information, incorrect values and other errors before analysing transactions.
•Provide an easy interface: Use Gradio so users can upload their files and interact with the assistant without needing to run Python code themselves.
•Handle errors and unclear questions: Give helpful messages when a file is incorrect or a question cannot be answered using the available data.
To make the assistant as effective as possible, I would recommend testing each feature with different transaction examples, checking that calculations are correct and making sure the AI does not make up financial information that is not supported by the user's data. Planning these features before coding will help keep the project organised and ensure the assistant meets its main purpose.”

What I kept, changed and why: I considered all that AI said would make my assistant easy to use while keeping it accurate and helpful. I used the different transaction examples, as it allowed me to calculate and see if what I got was the same as what AI was giving me.

What I rejected or corrected: I didn’t need to reject or correct anything as I was just seeking some understanding and advice on how to start the project. 





# Diary Entry 2: Creating the Spending Calculations – 3rd October 2026
What I was trying to do: I wanted to use Python and pandas to calculate total spending, spending by category and the biggest spending category.

AI prompt: I asked AI to help me create the spending calculations. It provided example code using pandas, including sum(), groupby() and idxmax().
"I am building the calculation section of my Personal Spending Assistant in Google Colab using Python and pandas. My transaction data has Description, Category and Amount columns. Help me write a simple function called spending_summary(df) that calculates the total amount spent, the total for each category, and the category with the highest spending. The function should use the actual data in the DataFrame rather than fixed numbers. Explain the code line by line in beginner-friendly language, show the expected output for Groceries $100, Transport $20 and Entertainment $30, and point out any assumptions or possible errors I should test for." 

Response: 

What I kept, changed and why: I kept these functions because they allowed me to calculate the spending information from my transaction data. The .sum() adds all the amounts together. The .groupby("Category") groups transactions with the same category. The .idxmax() finds the category with the highest total. The .max() returns the highest spending amount. And by having an empty-data check, the program doesn't try to analyse a file with no transactions, along with a negative-amount check so negative spending values are flagged for review. 
I used sample transactions for groceries, transport and entertainment to check whether the calculations matched my expected results.
What I rejected or corrected: When the category output included extra pandas information because pandas was displaying the data as a Series, which included additional details such as the data type and index. I changed the display to use categories.to_string() because it showed only the category results, making them easier to read. 
print("\nSpending by category:")
print(category_spending.to_string())

I also had to rerun a function after getting a NameError. This happened because the function had not been defined in the current session before I tried to use it, or the cell containing the function had not been run. This helped me understand the importance of running code cells in the correct order and making sure a function is defined before calling it.



# Diary Entry 3: Sample CSV Files – 4th October 2026
What I was trying to do: I wanted the program to read transaction information from a CSV file instead of relying only on data written directly in the code.
AI prompt: 
"For my Personal Spending Assistant, I need to work with transaction data stored in a CSV file. Can you help me create a sample CSV file so that I can understand the whole process before I create an actual one? The file will contain Description, Category and Amount columns. Keep the code consistent with a beginner-level Google Colab notebook. Please include .read_csv code along with printing the upload so that the user can see all their expenses.”

Response: 
What I kept, changed and why: I kept the CSV approach because it allowed me to understand how this all works. What I added was a validation afterwards. The validation allows the program to check the transaction data before calculating the results. If the validation function detects a problem, it won't run the spending calculations.

What I rejected or corrected: I didn’t need to change any of the code AI gave me as it was just a sample approach. 



# Diary Entry 4: Creating CSV Files 4th October 2026
What I was trying to do: After understanding and following an example with AI, I wanted to now create code where a user can upload their CSV file and the code reads it and provides an overview of expenses. 

AI Prompt: 
“For my Personal Spending Assistant, I need to work with transaction data stored in a CSV file. The file contains Description, Category and Amount columns. Explain how to create code where a user can upload their CSV. Keep the code functions similar to the example we did earlier today. Keep the code consistent with a beginner-level Google Colab notebook. Explain how I can check that the CSV loaded correctly and what could go wrong if a file is missing or the column names do not match. Please show how the CSV data connects to my existing function rather than creating a completely separate spending calculator.”

Response: 


What I kept, changed and why: I didn’t change any of the code, as it was similar to the sample. The files.upload() opens a file picker, allowing the user to choose a file from your computer. The io helps Python read the uploaded file's contents. The uploaded_files.keys() gets the name of the file you selected. The pd.read_csv() code is important as it reads the CSV data into a pandas DataFrame. And then the uploaded_df stores the transactions so we can analyse them.

What I rejected or corrected: I didn’t reject any of the code, but I did add a validation below to check the transaction data before calculating the results, just like I did for the sample. 



# Diary Entry 5: Creating the User Interface – 6th October 2026
What I was trying to do: I wanted to make my program easier to use by creating an interface where users could interact with the spending assistant.

AI Prompt: "I have already written a spending_summary(df) function and a check_transactions(df) validation function for my Personal Spending Assistant. I now want to make these features accessible through Gradio in Google Colab. I am not familiar with Gradio, so I need your help to build a simple interface that allows a non-programmer to upload a CSV file and receive their total spending, spending by category and highest-spending category. Reuse my existing functions rather than duplicating their logic. Explain how the uploaded file reaches the analysis function and make sure invalid or empty files produce a clear error message instead of crashing. Keep the code simple enough for me to explain in my assessment."

Response: Gradio can provide a simple interface so a user does not need to run each Python function manually. You can create a function that receives the uploaded file, loads it into pandas, validates the data and then displays the spending summary.
import gradio as gr

def greet_user(name):
    if name.strip() == "":
        return "Please enter your name."
    return "Hello, " + name + "! Welcome to your Personal Spending Assistant."

demo = gr.Interface(
    fn=greet_user,
    inputs=gr.Textbox(label="Enter your name"),
    outputs=gr.Textbox(label="Welcome message"),
    title="Personal Spending Assistant",
    description="Your tool for understanding your spending."
)

demo.launch(share=True


What I kept, changed and why: I kept Gradio because it allowed me to create an interface without building a separate website. I moved the basic welcome-message demo to the CSV analysis interface because the second version, where I allowed them to upload a CSV file, was more relevant to the assessment.
I changed the code to:
def analyse_csv(file):
    if file is None:
        return "Please upload a CSV file."

    try:
        data = pd.read_csv(file.name)

        # Check that the uploaded data is valid
        result = check_transactions(data)

        if result != "Transaction data looks good!":
            return result

        # Calculate the spending summary
        total, categories, biggest, amount = spending_summary(data)

        summary = f"Total spending: ${total:.2f}\n\n"
        summary += "Spending by category:\n"
        summary += categories.to_string()
        summary += f"\n\nBiggest category: {biggest} - ${amount:.2f}"

        return summary

    except Exception as error:
        return f"Could not read the file. Please upload a valid CSV. Details: {error}"

demo = gr.Interface(
    fn=analyse_csv,
    inputs=gr.File(label="Upload your transaction CSV", file_types=[".csv"], type="filepath"),
    outputs=gr.Textbox(label="Your spending summary", lines=8),
    title="Personal Spending Assistant",
    description="Upload your transaction CSV to analyse your spending."
)

demo.launch(share=True)


What I rejected or corrected: I did not keep the welcome message as the final interface because it did not analyse transactions. I tested the new interface with my sample CSV and checked that it displayed the total spending, category breakdown and biggest spending category, it did exactly that, so I kept the upgraded code with no welcome message.




# Diary Entry 6: Connecting Gemini – 11th October 
What I was trying to do: I wanted users to ask questions about their spending and get AI-generated answers based on their transaction information.
At this point of the assessment, I created a new Repository. I wanted to reformat my code and layout, so I created a new Repository and copied all my information into it. 

AI prompt: I asked AI how to connect the Gemini API to my Colab notebook. It guided me through installing the Gemini library, I then used the modules to add a API key in Colab Secrets and made sure to test the connection. It then provided code for sending a question to Gemini and displaying the response.
“I have a working spending summary function and a Gradio interface for my Personal Spending Assistant. I want to add Google's Gemini API so users can upload a CSV and ask questions about their spending. Help me connect Gemini using the google-genai library, and I will add an API key stored securely in Google Colab Secrets under GEMINI_API_KEY. The assistant must receive a summary calculated from the user's actual CSV data, answer finance-related questions using those figures, and respond appropriately to off-topic or unclear questions. Give me a clear system instruction that defines its role as a personal spending assistant. Explain the code in simple terms and show how to handle a failed API request without exposing the key."

Response:
 
def answer_spending_question(file, question):
    if file is None:
        return "Please upload your transaction CSV first."

    if question.strip() == "":
        return "Please enter a question about your spending."

    try:
        data = pd.read_csv(file.name)

        result = check_transactions(data)
        if result != "Transaction data looks good!":
            return result

        total, categories, biggest, amount = spending_summary(data)

        spending_information = f"""
        Total spending: ${total:.2f}

        Spending by category:
        {categories.to_string()}

        Biggest spending category: {biggest}
        Amount in biggest category: ${amount:.2f}
        """

        prompt = f"""
        You are a helpful personal spending assistant.

        Use only the spending information provided below to answer
        the user's question. Do not make up financial information.
        If the information is not enough to answer, say so.

        Spending information:
        {spending_information}

        User's question:
        {question}
        """

        response = client.models.generate_content(
            model="gemini-flash-latest",
            contents=prompt
        )

        return response.text

    except Exception as error:
        return "Something went wrong. Please check your CSV and try again."

demo = gr.Interface(
    fn=answer_spending_question,
    inputs=[
        gr.File(
            label="Upload your transaction CSV",
            file_types=[".csv"],
            type="filepath"
        ),
        gr.Textbox(
            label="Ask a question about your spending",
            placeholder="Which category did I spend the most on?"
        )
    ],
    outputs=gr.Textbox(
        label="Gemini's answer",
        lines=8
    ),
    title="Personal Spending Assistant",
    description="Upload your transactions and ask questions about your spending."
)

demo.launch(share=True)


What I kept, changed and why: I kept the Gemini integration because it added a question and answer feature to my spending assistant. I also kept the use of Colab Secrets so the API key was not written directly into my code. After the first code AI gave me, I added a test to see if the AI was working. 
prompt = "In one sentence, explain why tracking personal spending can be useful."

response = client.models.generate_content(
    model="gemini-flash-latest",
    contents=prompt
)

print(response.text)


What I rejected or corrected: I did not want Gemini to invent financial information or answer using information that was not in the transaction summary. I used a prompt instructing Gemini to answer using only the spending information provided and to say when there was not enough information to answer. I then tested the feature using my sample transactions. Which AI worked correctly and answered what I needed it to answer. 






# Diary Entry 7: Testing and Fixing Errors – 13th October 
What I was trying to do: I wanted to check that my program worked correctly with valid data and handled incorrect data appropriately.

AI prompt: I asked AI how to test my program using Python assert statements and how to check for invalid transaction data. It suggested tests for spending totals, category totals, missing columns, negative amounts and empty data.
"I am testing my Personal Spending Assistant. My project uses spending_summary(df) to calculate total spending, category totals and the highest-spending category, and check_transactions(df) to validate uploaded CSV data. Help me create assert-based tests that check exact expected results for a normal dataset and also test invalid inputs, including an empty DataFrame, a missing required column, a missing amount, a negative amount and an amount stored as text. Explain what each test is checking. If you identify a problem in my validation function, explain why it happens and suggest the smallest change needed to fix it. I need to understand the fix rather than simply copy code."

Response: 

# Test 5: Check that a missing column is detected
missing_column_df = pd.DataFrame({
    "Description": ["Supermarket"],
    "Amount": [60]
})

assert "Missing required column" in check_transactions(missing_column_df)
print("Test 5 passed: Missing columns are detected.")

# Test 6: Check that negative amounts are rejected
negative_df = pd.DataFrame({
    "Description": ["Supermarket"],
    "Category": ["Groceries"],
    "Amount": [-60]
})

assert "cannot be negative" in check_transactions(negative_df)
print("Test 6 passed: Negative amounts are rejected.")

# Test 7: Check that empty data is rejected
empty_df = pd.DataFrame(columns=["Description", "Category", "Amount"])

assert check_transactions(empty_df) == "Error: No transactions found."
print("Test 7 passed: Empty data is rejected.")

print("All invalid-data tests passed!")


What I kept, changed and why: I used some automated tests because they helped me check whether the program returned the expected results. I also tested what happened when a transaction had a missing amount. All tests showed the right outcome. 
Test 1 passed: Total spending is correct 
Test 2 passed: Category spending is correct 
Test 3 passed: Biggest category is correct
Test 4 passed: Valid transaction data is accepted 
Test 5 passed: Missing columns are detected 
Test 6 passed: Negative amounts are rejected 
Test 7 passed: Empty data is rejected 

What I rejected or corrected: I found that the original validation function did not explicitly reject missing amounts. I then asked AI how to correct this so I updated the check_transactions() code to check for missing amounts, descriptions and categories.
def check_transactions(df):
    # Check that the data is not empty
    if df.empty:
        return "Error: No transactions found."

    # Check that the required columns exist
    required_columns = ["Description", "Category", "Amount"]

    for column in required_columns:
        if column not in df.columns:
            return "Error: Missing required column: " + column

    # Check that descriptions and categories are not missing
    if df["Description"].isna().any() or df["Category"].isna().any():
        return "Error: Descriptions and categories cannot be empty."

    # Check that the amounts are numbers
    if not pd.api.types.is_numeric_dtype(df["Amount"]):
        return "Error: Amounts must be numbers."

    # Check that amounts are not missing
    if df["Amount"].isna().any():
        return "Error: Amounts cannot be empty."

    # Check that amounts are not negative
    if (df["Amount"] < 0).any():
        return "Error: Amounts cannot be negative."

    return "Transaction data looks good!"

Changed to this code.

I then ran another test to confirm that missing amounts were rejected. 
Create transaction data with a missing amount
missing_amount_df = pd.DataFrame({
    "Description": ["Supermarket", "Bus card"],
    "Category": ["Groceries", "Transport"],
    "Amount": [60, None]
})

print(check_transactions(missing_amount_df))

This made the validation more reliable.

