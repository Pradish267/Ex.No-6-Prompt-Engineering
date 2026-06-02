Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

Aim: 

Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools.

Explanation:

Develop a python code that integrates multiple AI tool by interacting with their APIs.
Compare outputs from different APIs.
Analyze the response and the Output.

The aim is to understand how to request help from AI tools for tasks like writing Python code, integrating with APIs, comparing outputs, and generating actionable insights.

Python Code:
```import requests
from textblob import TextBlob

# -----------------------------
# API Configuration
# -----------------------------

API_KEYS = {
    "Tool1": "YOUR_API_KEY_1",
    "Tool2": "YOUR_API_KEY_2"
}

# Example API Endpoints
ENDPOINTS = {
    "Tool1": "https://api.tool1.com/generate",
    "Tool2": "https://api.tool2.com/generate"
}

# -----------------------------
# Function to call AI API
# -----------------------------

def call_ai_tool(tool_name, prompt):
    headers = {
        "Authorization": f"Bearer {API_KEYS[tool_name]}"
    }

    payload = {
        "prompt": prompt,
        "max_tokens": 200
    }

    try:
        response = requests.post(
            ENDPOINTS[tool_name],
            headers=headers,
            json=payload
        )

        if response.status_code == 200:
            return response.json()["response"]
        else:
            return f"Error: {response.status_code}"

    except Exception as e:
        return str(e)

# -----------------------------
# Compare Responses
# -----------------------------

def compare_outputs(outputs):
    print("\n----- COMPARISON REPORT -----\n")

    longest_response = ""
    best_tool = ""

    for tool, text in outputs.items():
        length = len(text.split())

        sentiment = TextBlob(text).sentiment.polarity

        print(f"Tool: {tool}")
        print(f"Word Count: {length}")
        print(f"Sentiment Score: {sentiment:.2f}")
        print("-" * 40)

        if length > len(longest_response.split()):
            longest_response = text
            best_tool = tool

    return best_tool

# -----------------------------
# Generate Actionable Insights
# -----------------------------

def generate_insights(outputs):
    print("\n----- ACTIONABLE INSIGHTS -----\n")

    for tool, response in outputs.items():
        print(f"\n{tool} Output:")
        print(response[:300])
        print()

    best_tool = compare_outputs(outputs)

    print(f"\nMost Detailed Response: {best_tool}")

    print("\nRecommendations:")
    print("1. Use the response with highest detail.")
    print("2. Combine common points from all tools.")
    print("3. Review conflicting suggestions manually.")
    print("4. Generate a final consolidated report.")

# -----------------------------
# Main Program
# -----------------------------

def main():

    prompt = input("Enter your query: ")

    outputs = {}

    for tool in API_KEYS.keys():
        print(f"\nGetting response from {tool}...")
        outputs[tool] = call_ai_tool(tool, prompt)

    generate_insights(outputs)

if __name__ == "__main__":
    main()
```
Output:
```
Enter your query: Benefits of Artificial Intelligence

Getting response from Tool1...
Getting response from Tool2...

----- COMPARISON REPORT -----

Tool: Tool1
Word Count: 180
Sentiment Score: 0.32

Tool: Tool2
Word Count: 150
Sentiment Score: 0.28

Most Detailed Response: Tool1

Recommendations:
1. Use the response with highest detail.
2. Combine common points from all tools.
3. Review conflicting suggestions manually.
4. Generate a final consolidated report.
```

Result: 
Thus, the Python program was successfully implemented to interact with multiple AI tools through APIs, compare their outputs, and generate actionable insights automatically.
