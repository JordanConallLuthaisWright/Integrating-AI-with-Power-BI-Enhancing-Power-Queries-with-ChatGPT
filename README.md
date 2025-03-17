# AI Powered-Text-Categorization-in-Power-BI-Leveraging-ChatGPT-for-Song-Lyrics-Analysis

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
| `Eminem_Lyrics_Analysis.ipynb` | Jupyter Notebook with a detailed walkthrough of the analysis. |
| `Eminem_Lyrics.csv` | Dataset containing the lyrics of Eminem's songs. |

For this test project, the dataset consists of **Eminem's song lyrics** (found on kaggle), which includes the following columns:
- **Song Name**: The name of the song.
- **Lyrics**: The text of the song’s lyrics.

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

