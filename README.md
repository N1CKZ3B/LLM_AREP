# LLM_AREP
## Nicolas Achuri Macias

A simple translation service built with LangChain, FastAPI, and OpenAI's GPT models. This project demonstrates how to create a translation API server and client using LangChain's Runnable interfaces.

## Architecture

The project consists of three main components:

1. **Server (`server.py`)**
   - Built with FastAPI and LangChain
   - Exposes a translation endpoint at `/chain`
   - Uses OpenAI's GPT models for translation
   - Implements a chain of:
     - Prompt Template
     - Language Model
     - Output Parser

2. **Client (`client.py`)**
   - Implements a simple client using LangServe's RemoteRunnable
   - Connects to the local server to perform translations

3. **Development Notebook (`project.ipynb`)**
   - Contains the development process and testing
   - Shows step-by-step implementation of the components

## Prerequisites

- Python 3.11 or higher
- OpenAI API key

## Installation

1. Clone the repository:
```bash
git clone https://github.com/N1CKZ3B/LLM_AREP.git
cd LLM_AREP
```

2. Create and activate a virtual environment:
```bash
python -m venv .venv
# On Windows
.venv\Scripts\activate
# On Unix or MacOS
source .venv/bin/activate
```

3. Install the required dependencies:
```bash
pip install langchain
pip install langchain-openai
pip install "langserve[all]"
```

## Configuration

1. Set up your OpenAI API key:
   - The server will prompt for your API key when starting
   - Alternatively, you can set it as an environment variable:
```bash
# On Windows
set OPENAI_API_KEY=your-api-key-here
# On Unix or MacOS
export OPENAI_API_KEY=your-api-key-here
```

## Running the Application

1. Start the server:
```bash
python server.py
```
The server will start on `http://localhost:8000`

2. In a separate terminal, run the client:
```bash
python client.py
```

## API Usage

### Server Endpoints

- **Translation Endpoint**: `POST http://localhost:8000/chain/`
  - Request Body:
    ```json
    {
        "language": "string",
        "text": "string"
    }
    ```
  - Example Response:
    ```json
    "translated text"
    ```

### Client Usage

```python
from langserve import RemoteRunnable

# Create client
remote_chain = RemoteRunnable("http://localhost:8000/chain/")

# Perform translation
response = remote_chain.invoke({
    "language": "italian",
    "text": "hi"
})
print(response)  # Output: "Ciao"
```

## Example Screenshots

### Server Running
```
INFO:     Started server process [12345]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://localhost:8000
```

### Translation Request
```python
# Example request
response = remote_chain.invoke({
    "language": "japanese",
    "text": "roronoa zoro"
})
print(response)  # Output: "ロロノア・ゾロ"
```

## Project Structure
```
LLM_AREP/
├── .venv/                  # Virtual environment
├── server.py              # FastAPI server implementation
├── client.py              # Client implementation
├── project.ipynb          # Development notebook
└── README.md             # This file
```

## Technical Details

- The translation chain is composed of:
  1. A prompt template that formats the translation request
  2. The GPT model that performs the translation
  3. A string output parser that formats the response

- The server uses FastAPI's automatic OpenAPI documentation, available at:
  - Swagger UI: `http://localhost:8000/docs`
  - ReDoc: `http://localhost:8000/redoc`

## License

This project is licensed under the MIT License - see the LICENSE file for details.
