# AI-Driven Code Insight Platform

This repository contains the Code Explanation App, a tool designed to provide clear and concise explanations of code snippets. The app leverages the capabilities of the PaLM 2 (Legacy) model to generate explanations.

# Features
Interactive Interface: Users can input any code snippet to receive an explanation.

Text Generation: Utilizes the text-bison-001 model for generating explanations and responses.

Flexible Output: Adjust the temperature and token limits to control the randomness and length of the generated text.

Gradio Integration: Easy-to-use web interface powered by Gradio for seamless user interaction.

# Notebook Content

# Setup and Model Initialization

# The notebook begins with setting up the necessary environment and loading the required models:

import palm
import os

# API Key setup
api_key = os.getenv("PALM_API_KEY")
palm.configure(api_key=api_key)

# Listing available models
models = [model.name for model in palm.list_models() if model.name == "models/text-bison-001"]

# Simple Chatbot

An example of using the model to generate text based on a prompt:

# Define the input prompt
prompt1 = "Why is the Sky blue? Provide answers in bullet format in clear and concise manner."

prompt2 = "Why is Generative AI growing so much?"

# Generate the text

completion = palm.generate_text(
    model = models[0],
    prompt = prompt1,
    temperature = 1,
    max_output_tokens = 500
)
print(completion.result)

# Web Interface

The app provides a web-based interface using Gradio for ease of use:

import gradio as gr

# Define the function for generating explanations

def get_completion(text):
    completion = palm.generate_text(
        model=models[0],
        prompt=text,
        temperature=0.7,
        max_output_tokens=500
    )
    return completion.result

# Setup the Gradio interface

iface = gr.Interface(
    fn=get_completion,
    inputs=[gr.Textbox(label="Insert Code Snippet")],
    outputs=[gr.Textbox(label="Explanation Here")],
    title="Code Sensai"
)
iface.launch(share=True, debug=True)

# How to Run

Clone the Repository:

git clone https://github.com/your_username/code-explanation-app.git
cd code-explanation-app

# Install Dependencies:

Ensure you have all the required packages installed. You can use pip to install them:

pip install -r requirements.txt


# Set Up API Key:

Make sure you have your PaLM API key set up in your environment variables:

export PALM_API_KEY='your_api_key'

# Run the Notebook:
Open the Jupyter Notebook and run all cells to ensure everything is set up correctly.

# Launch the Gradio Interface:

Run the Gradio interface cell to start the web application. You will get a shareable link to interact with the app.

# Contributions
Feel free to fork this repository, make improvements, and submit pull requests. For major changes, please open an issue first to discuss what you would like to change.
