## Ex:1 Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

# AIM:
To design and implement a Python function for calculating the volume of a cylinder,  
integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

## PROBLEM STATEMENT:
Design and implement a system where a user can input dimensions of a cylinder (radius and height),  
and the system calculates its volume by invoking a Python function using the function-calling capabilities of an LLM.


## DESIGN STEPS:

1. Import necessary libraries, including OpenAI for LLM integration and math for mathematical operations.
2. Define a Python function to calculate the volume of a cylinder based on its radius and height.
3. Integrate the function into an LLM-based chat completion system with function-calling capabilities.



## PROGRAM:

```
import os
import openai

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) # read local .env file
openai.api_key = os.environ['OPENAI_API_KEY']
import math
def calculate_cylinder_volume(radius, height):
    return math.pi*radius**2*height
functions=[
    {
        "name": "calculate_cylinder_volume",
        "description": "Calculate the volume of a cylinder given its radius and height",
        "parameters": {
            "type": "object",
            "properties": {
                "radius": {
                    "type": "number",
                    "description": "The radius of the cylinder"
                },
                "height": {
                    "type": "number",
                    "description": "The height of the cylinder"
                }
            },
            "required": ["radius","height"]
        }
    }
]
messages=[
    {
        "role": "user",
        "content": "What is the volume of the cylinder with radius 5 and height 10?"
    }
]
response=openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=messages,
    functions=functions,
    function_call="auto"
)
print(response)
import json
message=response["choices"][0]["message"]
arguments=json.loads(message["function_call"]["arguments"])
print("Arguments are:",arguments)
radius=arguments["radius"]
height=arguments["height"]
print(f"The volume of the cylinder is {calculate_cylinder_volume(radius,height):.2f}")
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/da93f8d0-0cb3-417b-8d76-99d84230795f)
## RESULT:
Hence,the python program to design and implement a Python function for calculating the volume of a cylinder,  
integrating it with a chat completion system utilizing the function-calling feature of a large language model (LLM) is written successfully and executed.
