## Ex:5 Design and Implementation of a Multidocument Retrieval Agent Using LlamaIndex

### AIM:
To design and implement a multidocument retrieval agent using LlamaIndex to extract and synthesize information from multiple research articles, and to evaluate its performance by testing it with diverse queries, analyzing its ability to deliver concise, relevant, and accurate responses.

### PROBLEM STATEMENT:
The challenge is to develop an agent that can efficiently retrieve and synthesize information from a large corpus of documents, ensuring that it answers queries with precision and relevance, leveraging LlamaIndex for effective retrieval and summarization.
### DESIGN STEPS:

#### STEP 1:
Gather a set of research articles or documents relevant to the topic. Preprocess the data by converting the articles into a suitable format (e.g., plain text or structured format). Tokenize the content and remove any irrelevant or noisy information.
#### STEP 2:
Use LlamaIndex (formerly known as GPT Index) to create an index for the documents.LlamaIndex will help build an optimized index for efficient retrieval, making it easy to query multiple documents at once. Incorporate features like semantic search to improve relevance and accuracy of retrieval.
#### STEP 3:
Develop the query interface where users can input questions related to the research articles. Integrate the query interface with the LlamaIndex-powered retrieval system.
#### STEP 4:
Test the system with a range of diverse queries to evaluate its performance in terms of accuracy, relevance, and conciseness of responses. Collect feedback and refine the system based on test results.
### PROGRAM:
```py
urls = [
    "https://openreview.net/pdf?id=VtmBAGCN7o",
    "https://openreview.net/pdf?id=6PmJoRfdaK",
    "https://openreview.net/pdf?id=hSyW5go0v8",
]

papers = [
    "metagpt.pdf",
    "longlora.pdf",
    "selfrag.pdf",
]

from utils import get_doc_tools
from pathlib import Path

paper_to_tools_dict = {}
for paper in papers:
    print(f"Getting tools for paper: {paper}")
    vector_tool, summary_tool = get_doc_tools(paper, Path(paper).stem)
    paper_to_tools_dict[paper] = [vector_tool, summary_tool]

from llama_index.llms.openai import OpenAI

llm = OpenAI(model="gpt-3.5-turbo")

from llama_index.core.agent import FunctionCallingAgentWorker
from llama_index.core.agent import AgentRunner

agent_worker = FunctionCallingAgentWorker.from_tools(
    initial_tools, 
    llm=llm, 
    verbose=True
)
agent = AgentRunner(agent_worker)

response = agent.query(
    "Tell me about the evaluation dataset used in LongLoRA, "
    "and then tell me about the evaluation results"
)

response = agent.query("Give me a summary of both Self-RAG and LongLoRA")
print(str(response))
```
### OUTPUT:
![image](https://github.com/user-attachments/assets/4dca9576-925b-4764-a972-b814f781b5f0)
![image](https://github.com/user-attachments/assets/de068029-cd1d-4895-a27e-8a45f569ed0b)


### RESULT:
The system successfully retrieves and synthesizes relevant information from multiple documents, providing concise and relevant answers to the user's query. Performance is evaluated based on the accuracy, relevance, and coherence of the responses.
