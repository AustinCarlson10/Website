<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Website Analyzer</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100">
    <div class="container mx-auto px-4 py-8">
        <h1 class="text-3xl font-bold text-center mb-8">Website Analyzer</h1>
        <div class="max-w-md mx-auto bg-white p-8 rounded shadow">
            <label for="urlInput" class="block text-gray-700 text-sm font-bold mb-2">Enter a URL:</label>
            <input id="urlInput" type="text" placeholder="https://example.com" class="w-full px-3 py-2 mb-4 border rounded" />
            <button id="analyzeButton" class="w-full bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                Analyze Website
            </button>
        </div>
        <div id="results" class="max-w-2xl mx-auto mt-8"></div>
    </div>
    <script>
        document.getElementById('analyzeButton').addEventListener('click', function() {
            const urlInput = document.getElementById('urlInput').value.trim();

            if (!urlInput) {
                alert('Please enter a URL.');
                return;
            }

            // Show loading indicator
            const resultsDiv = document.getElementById('results');
            resultsDiv.innerHTML = '<p class="text-center text-gray-500">Analyzing...</p>';

            fetch('/analyze', { // Ensure your backend endpoint matches this URL
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({ url: urlInput })
            })
            .then(response => {
                if (!response.ok) {
                    throw new Error('Network response was not ok');
                }
                return response.json();
            })
            .then(data => {
                displayResults(data);
            })
            .catch(error => {
                resultsDiv.innerHTML = `<p class="text-red-500">An error occurred: ${error.message}</p>`;
            });
        });

        function displayResults(data) {
            const resultsDiv = document.getElementById('results');

            let html = `
                <h2 class="text-2xl font-bold mb-4">Analysis Results</h2>
                <h3 class="text-xl font-semibold mt-4">Pros:</h3>
                <ul class="list-disc pl-5">
                    ${data.pros.length > 0 ? data.pros.map(item => `<li>${item}</li>`).join('') : '<li>No pros found.</li>'}
                </ul>
                <h3 class="text-xl font-semibold mt-4">Cons:</h3>
                <ul class="list-disc pl-5">
                    ${data.cons.length > 0 ? data.cons.map(item => `<li>${item}</li>`).join('') : '<li>No cons found.</li>'}
                </ul>
                <h3 class="text-xl font-semibold mt-4">Generated Message:</h3>
                <p class="mt-2 whitespace-pre-line">${data.ai_generated_text}</p>
            `;

            resultsDiv.innerHTML = html;
        }
    </script>
</body>
</html>
```

```python
import json
import re
import os
import requests
import openai
from flask import Flask, request, jsonify
from bs4 import BeautifulSoup

app = Flask(__name__)

def analyze_page(soup):
    pros = []
    cons = []

    page_text = soup.get_text(strip=True)
    if len(page_text) < 200:
        cons.append("Your webpage feels a bit short. Adding more content could help keep visitors interested.")
    else:
        pros.append("I love how your website has plenty of content to keep visitors engaged.")

    nav = soup.find('nav')
    if nav:
        pros.append("Your navigation is clear and easy to use, making it simple for visitors to find what they need.")
    else:
        cons.append("Adding a navigation bar could help visitors navigate your site more easily.")

    viewport = soup.find('meta', attrs={'name': 'viewport'})
    if viewport:
        pros.append("Great job on making your website mobile-friendly!")
    else:
        cons.append("Consider adding a viewport meta tag to improve mobile responsiveness.")

    anchors_no_href = [a for a in soup.find_all('a') if not a.get('href')]
    if anchors_no_href:
        cons.append("I noticed some links that don’t go anywhere. It might confuse folks who try to click them.")
    else:
        pros.append("All of your links are working correctly, making navigation seamless for your visitors.")

    images = soup.find_all('img')
    if images:
        pros.append("Nice touch with the images; they add a lot of personality to your website.")
        images_without_alt = [img for img in images if not img.get('alt')]
        if images_without_alt:
            cons.append("Some of your images don’t have alt descriptions. That can make it tougher for everyone to enjoy them.")
    else:
        cons.append("It looks like there aren't any images. Including a few could make your site more visually appealing.")

    title = soup.find('title')
    if title and len(title.text) > 5:
        pros.append("Your webpage has a clear and descriptive title, which is great for SEO.")
    else:
        cons.append("Consider adding a more descriptive title tag to improve your site's SEO.")

    return pros, cons

@app.route('/analyze', methods=['POST'])
def analyze():
    try:
        event_data = request.get_json()
    except Exception as e:
        return jsonify({'error': 'Invalid JSON in request body'}), 400

    url = event_data.get('url')
    recipient_name = event_data.get('recipient_name', 'Valued Website Owner')

    if not url:
        return jsonify({'error': 'URL is required'}), 400

    try:
        response = requests.get(url, timeout=10)
        response.raise_for_status()
    except requests.exceptions.RequestException as e:
        return jsonify({'error': 'Failed to fetch the URL'}), 400

    soup = BeautifulSoup(response.content, 'html.parser')
    text = soup.get_text()

    phone_numbers = re.findall(r'\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}', text)
    emails = re.findall(r'[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}', text)

    pros, cons = analyze_page(soup)

    pros_text = "\n- ".join(pros) if pros else "I couldn’t find any specific positives, but I’m sure there’s something to love!"
    cons_text = "\n- ".join(cons) if cons else "I didn’t notice any areas that really need improvement!"

    openai.api_key = os.getenv('OPENAI_API_KEY')  # Make sure to set your OpenAI API key in environment variables

    user_name = os.getenv('USER_NAME', 'Austin Carlson')
    user_age = os.getenv('USER_AGE', '16')

    FIXED_CONCLUSION_TEMPLATE = (
        f"Hi {recipient_name},\n\n"
        f"My name is {user_name}, and I'm {user_age} years old. As part of a personal project, I recently built your website and would love to get your feedback. "
        "My goal is to analyze business websites to identify strengths and areas for improvement. I’d really appreciate any thoughts you have on what’s working well and what could be enhanced.\n\n"
        "Looking forward to your insights!\n\n"
        "Thank you!\n"
        f"{user_name}"
    )

    prompt = (
        f"**Here are some things I noticed:**\n\n"
        f"**Pros:**\n- {pros_text}\n\n"
        f"**Cons:**\n- {cons_text}\n"
        "\nPlease provide any additional feedback or suggestions you might have."
    )

    try:
        ai_response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=[
                {
                    "role": "system",
                    "content": (
                        "You are an AI assistant that crafts friendly, courteous messages. "
                        "Always begin the message with a personal introduction that includes the user's name and age. "
                        "Use warm and engaging language while referencing the pros and cons provided."
                    )
                },
                {
                    "role": "user",
                    "content": prompt
                }
            ],
            temperature=0.7,
            max_tokens=300,
        )
        ai_generated_text = ai_response['choices'][0]['message']['content']
    except Exception as e:
        return jsonify({'error': str(e)}), 500

    fixed_conclusion = FIXED_CONCLUSION_TEMPLATE

    complete_message = f"{ai_generated_text.strip()}\n\n{fixed_conclusion}"

    result = {
        'phone_numbers': phone_numbers,
        'emails': emails,
        'pros': pros,
        'cons': cons,
        'ai_generated_text': complete_message
    }

    return jsonify(result), 200

if __name__ == '__main__':
    app.run(debug=True)
