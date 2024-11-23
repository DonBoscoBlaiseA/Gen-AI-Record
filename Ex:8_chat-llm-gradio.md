## Development and Deployment of a 'Chat with LLM' Application Using the Gradio Blocks Framework

### AIM:
To design and deploy a "Chat with LLM" application by leveraging the Gradio Blocks UI framework to create an interactive interface for seamless user interaction with a large language model.

### PROBLEM STATEMENT:
The objective is to develop an intuitive and interactive interface that enables users to communicate with a large language model (LLM) effectively. The application should handle user inputs, generate responses from the LLM, and display the results in real-time.
### DESIGN STEPS:

#### STEP 1:Set Up the Environment
+ Install the necessary libraries, such as gradio and transformers.
+ Choose an appropriate LLM (e.g., OpenAI's GPT, Hugging Face's GPT-2/3.5/4).
+ Ensure GPU support for faster inference, if required.
#### STEP 2:Create the Gradio Blocks Interface
+ Use gr.Blocks to design a modular and interactive layout.
+ Define the components such as Textbox for user input, Chatbot for displaying messages, and Button for interaction.

#### STEP 3: Integrate the LLM with the Interface
+ Test the application locally to ensure smooth functionality.
+ Deploy the app using platforms like Hugging Face Spaces, Streamlit Cloud, or a custom server.

### PROGRAM:
```
import gradio as gr
from transformers import AutoModelForCausalLM, AutoTokenizer

# Load the model and tokenizer
model_name = "gpt2"  # Replace with your LLM
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name)

# Function to interact with the model
def chat_with_llm(user_input):
    inputs = tokenizer.encode(user_input, return_tensors="pt")
    outputs = model.generate(inputs, max_length=150, num_return_sequences=1, pad_token_id=tokenizer.eos_token_id)
    response = tokenizer.decode(outputs[0], skip_special_tokens=True)
    return response

# Gradio interface using Blocks
with gr.Blocks() as chat_interface:
    gr.Markdown("### Chat with LLM")
    with gr.Row():
        with gr.Column():
            user_input = gr.Textbox(placeholder="Type your message here...")
            send_button = gr.Button("Send")
        with gr.Column():
            chatbot = gr.Chatbot()
    
    # Define interaction
    send_button.click(chat_with_llm, inputs=user_input, outputs=chatbot)
    
# Launch the interface
chat_interface.launch()
```
### OUTPUT:
![image](https://github.com/user-attachments/assets/81c54b26-5f0c-4180-b095-b1a68115ab61)

### RESULT:
The "Chat with LLM" application was successfully designed and deployed. The Gradio Blocks framework provided a user-friendly interface, ensuring seamless communication with the large language model.
