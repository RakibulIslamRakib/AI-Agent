# AI-Agent
INtroduction to Agentic AI development

//install depedencies

!pip install -U langchain langchain-core langchain-openai langgraph

//inject depedencies
 
from langchain_core.tools import tool // agent will use these tools for response , ie: query for a customer bank account current balence
from langchain_openai import ChatOpenAI
from langgraph.prebuilt import create_react_agent // reactive agent that will react using the llm and tools
import math

model = ChatOpenAI(openai_api_key = "<your_apikey>", model = "gpt-4o-mini") // initializing llm model

// these are the tools (custom function)
@tool
def add_numbers(a: float, b: float) -> float:
    """Adds two numbers together."""
    return a + b

@tool
def multiply_numbers(a: float, b: float) -> float:
    """multiply two numbers together."""
    return a + b

@tool
def square_root(x: float) -> float:
    """Returns the square root of a number."""
    return math.sqrt(x)

@tool
def greet(name: str) -> str:
    """Greets the user by name."""
    return f"Hello {name}! How can I assist you today?"
tools = [add_numbers, square_root, greet]


agent = create_react_agent(model, tools)

query = "what is (2+8) multiplied by 99?"

response = agent.invoke({
    "messages":[
        ("human",query)
    ]
})

print(response['message'][-1].content)

https://colab.research.google.com/drive/1Y33wEqZwLEwkBIFt_ezlwD39Z7W6wcQy?usp=sharing
