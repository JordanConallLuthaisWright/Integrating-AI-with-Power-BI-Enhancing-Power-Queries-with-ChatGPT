# AI Powered Text Categorization in Power BI Leveraging ChatGPT for Song Lyrics Analysis

## Overview
In this project, we explore the integration of OpenAI's **ChatGPT** with **Power BI**, specifically within **Power Query**. The goal was to leverage the power of AI to enhance the data transformation process, making it more efficient and insightful. Using a dataset of **Eminem’s song lyrics**, we categorized each song based on its lyrics with the help of ChatGPT, showcasing the potential for AI-assisted data analysis.

This integration demonstrates how AI can support Power BI users in automating categorization tasks, improving text analysis, and enabling deeper insights within their datasets. This project was a test to explore the efficient relationship between Power Query and AI, with potential future applications across various industries.

---

## Technical Skills and Tools
### 1. **Power Query (M Language)**
Power Query is an essential tool within Power BI for data transformation. It allows users to clean, transform, and prepare data in a way that suits their analytical needs. By integrating AI with Power Query, you can extend its capabilities to handle more complex data tasks such as natural language processing (NLP), text categorization, and sentiment analysis.

### 2. **ChatGPT API**
OpenAI’s ChatGPT API, particularly models like **GPT-4**, can be used for more advanced analyses like **text summarization**, **categorization**, and **question answering**. By integrating this API with Power BI, Power Query can be used to send data to AI models, process it, and return intelligent outputs.

### 3. **Power BI**
Power BI itself is a powerful data visualization and reporting tool. When combined with AI, Power BI can transform data in ways that would have been time-consuming or even impossible to do manually. The integration of AI can automate processes that involve large volumes of unstructured text, such as categorizing song lyrics or summarizing customer feedback.

---

## Dataset

## Files in This Repository  
| File | Description |
|------|------------|
| `Chatgpt_PowerBI_analysis.pbix` | PowerBI project file of project. |
| `Eminem_Lyrics.csv` | Dataset containing the lyrics of Eminem's songs taken from kraggle.com. |
| `Tutorial_Walkthrough_Chatgpt_PowerBI.mp4` | Walkthrough of how to impliment AI into power query. |
| `Tutorial_Walkthrough_Chatgpt_PowerBI_cont.mp4` | ^^^ |

For this test project, the dataset consists of **Eminem's song lyrics** (found on kaggle), which includes the following columns:
- **Album_name**
- **Song_name**
- **Lyrics**
- **Album_URL**
- **Views**
- **Release_Date**
- ***Song_Category*** <- The mission of this project using AI to query. 

This dataset was chosen to explore the potential of AI in categorizing text based on thematic content.

---

## Relevance of AI Integration into Power BI

### 1. **Text Analysis and Categorization**
Traditionally, text analysis and categorization tasks in Power BI are labor-intensive. However, with AI integration, these tasks become significantly more efficient. In this case, **ChatGPT** was used to analyze the song lyrics and categorize each song into a one-word genre. By leveraging AI, users can automate text classification tasks that would otherwise require manual intervention, saving time and effort.

In the context of **Power BI**, AI can be used to categorize, summarize, and extract themes from large datasets that contain text, such as customer reviews, feedback, product descriptions, or social media posts.

### 2. **Enhancing Data Transformation with AI**
Power Query is a powerful tool for transforming data into a structured format for analysis. By integrating AI with Power Query, users can handle more sophisticated tasks, such as:
- **Natural Language Processing (NLP)**: AI models like ChatGPT can analyze and understand natural language, making it possible to categorize and summarize text data in real-time.
- **Sentiment Analysis**: AI can be used to determine the sentiment (positive, negative, neutral) of customer reviews or social media posts, allowing businesses to understand customer satisfaction or market sentiment.
- **Text Summarization**: AI can summarize long text fields, such as articles or customer feedback, into concise summaries, which can then be used for more focused analysis.

By adding AI to Power Query, Power BI users can enhance their data transformation capabilities and create more meaningful visualizations and reports without manually processing large datasets.

### 3. **Efficient Decision-Making**
AI-powered analyses offer a significant boost to the decision-making process by automating tasks that would typically take a lot of time. For example, categorizing song lyrics or customer feedback using AI provides valuable insights that can guide marketing, content strategy, and customer relationship management (CRM). With AI integration in Power BI, businesses can unlock actionable insights much faster, allowing them to respond to market changes in real time.

### 4. **Advanced Data Automation**
One of the most compelling advantages of integrating AI into Power BI is the ability to automate complex workflows. For instance, AI can:
- Automatically categorize new data as it arrives.
- Identify emerging trends and patterns.
- Provide intelligent recommendations based on data analysis.

By reducing the manual effort required to analyze text or large volumes of unstructured data, AI accelerates the data transformation process, enabling more timely and data-driven decisions.

---

## Power Query M Code for AI Integration

![AI integrated in Power Query within PowerBI](images/AI%20integrated%20in%20query%20(PowerBI).png)

Below is the Power Query M code used to integrate **ChatGPT** into Power Query for categorizing the song lyrics dataset:

```m
(promptQuestion as text, promptInput as text) =>
let
    // Your OpenAI API endpoint
    apiUrl = "https://api.openai.com/v1/chat/completions",

    // Your OpenAI API Key (replace with your actual API key)
    apiKey = "your-api-key-here",

    // Define the headers for the API request
    headers = [
        #"Content-Type" = "application/json",
        #"Authorization" = "Bearer " & apiKey
    ],

    // Define the request body for the chat-based models (e.g., GPT-4)
    requestBody = Json.FromValue([
        model = "gpt-4", 
        messages = {
            [role = "system", content = "You are a helpful assistant."],
            [role = "user", content = promptQuestion & " " & promptInput]
        },
        max_tokens = 50
    ]),

    // Send the HTTP request to OpenAI API with POST method
    response = Web.Contents(apiUrl, [
        Headers = headers,
        Content = requestBody
    ]),

    // Parse the JSON response
    responseJson = Json.Document(response),

    // Extract the relevant part of the response (adjust as needed)
    completionText = responseJson[choices]{0}[message][content]
in
    completionText

```

---

The Power Query M code is used to call the ChatGPT API for each song’s lyrics and assign a one-word category. The key part of the code is:

```m
= Table.AddColumn(#"Removed Top Rows", "Song Category", each chatGPT("assign a one-word category to this song lyrics:", [Lyrics]))
```
(This Power Query step adds a new column called "Song Category", where each song is automatically assigned a one-word genre or category based on its lyrics.)

---

## Outcome
The outcome of this integration is a new column in the dataset, **"Song Category"**, where each song is automatically assigned a one-word genre or category based on its lyrics. This AI-assisted categorization saves time and ensures that large datasets can be processed efficiently.

---

## Future Applications
The integration of AI into Power BI's Power Query offers exciting possibilities for data analysis:

- **Customer Feedback Analysis**: Automatically categorize customer reviews or social media posts by sentiment or theme.
- **Text Summarization**: Create summaries for long text fields, making it easier to digest large amounts of information.
- **Automated Reporting**: Generate automated reports with AI-powered insights that require minimal human intervention.

By integrating AI into Power BI, businesses can transform their data transformation and analysis workflows, enabling them to unlock more actionable insights from their data.

---

## Instructions to Replicate the Project

### Step 1: Retrieve Your OpenAI API Key
To integrate OpenAI's API with Power BI, you first need an API key from OpenAI. Follow these steps to obtain your own API key:

1. **Create an OpenAI Account**:
   - Visit [OpenAI's platform page](https://platform.openai.com/signup).
   - Sign up for a new account or log in if you already have one.

2. **Access the API Key**:
   - Once logged in, go to the **API Keys** section by navigating to [API Keys](https://platform.openai.com/account/api-keys) from your dashboard.
   - If you don't have any API keys, click on the **"Create new secret key"** button.
   - A new API key will be generated for you. **Copy the API key** (you’ll need it in the next steps).

3. **Save Your API Key**:
   - Keep the key in a secure place (you'll use it to authenticate your requests to the OpenAI API).

### Step 2: Set Up Power BI and Power Query
Now that you have your API key, you can integrate it with Power BI:

1. **Open Power BI Desktop**:
   - Open **Power BI Desktop** and go to **Transform Data** to open Power Query Editor.

2. **Create a Blank Query**:
   - In the Power Query Editor, click on **New Source** and select **Blank Query**.

3. **Open the Advanced Editor**:
   - With the blank query selected, click on **Advanced Editor** and paste the Power Query M code provided earlier. Make sure to replace the placeholder `"your-api-key-here"` with the actual API key you obtained from OpenAI.

### Step 3: Adjust Your Dataset

1. **Prepare Your Dataset**:
   - Ensure that your dataset is ready for analysis, with a column that contains the text data (e.g., **Song Lyrics**).
   - You can import your dataset from a CSV file, Excel sheet, or other data sources.

2. **Apply the Power Query Code**:
   - Modify the Power Query M code to call the ChatGPT API and categorize each song based on its lyrics. The key part of the code is to add the **"Song Category"** column using the following Power Query code:

3. **Run the Query**
4. **Visualize the Results**
    - Once the data is loaded, you can use Power BI’s visualization tools to display the categorized song data. For example, you can create a **bar chart** showing how many songs fall into each category.

---

By following these steps, you can replicate this project, use ChatGPT to categorize text in Power BI, and unlock deeper insights from your data.

---

## **Contact & Contributions**  
Feel free to explore and contribute. If you have any suggestions, reach out or submit a pull request.  

- **Email**: [jordan.c.l.wright@gmail.com](mailto:jordan.c.l.wright@gmail.com)  

---

### **Author:** Jordan  
[GitHub Profile](https://github.com/JordanConallLuthaisWright)



