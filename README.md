# llm-pdf-chatbot

multipdf chatbot using gemini

explanation of the code ->

1. Import Libraries:
   - The code starts by importing necessary libraries for various functionalities:
     - Streamlit for the web interface
     - PyPDF2 for PDF handling
     - Langchain components for text processing and AI interactions
     - OS and dotenv for environment variable management
     - Google's generative AI libraries

2. Environment Setup:
   - Load environment variables from a .env file
   - Retrieve the Google API key
   - Configure Google's generative AI with the API key

3. PDF Text Extraction (get_pdf_text function):
   - Takes a list of PDF documents as input
   - For each PDF:
     - Creates a PdfReader object
     - Iterates through each page
     - Extracts text from the page
   - Combines all extracted text into a single string
   - Returns the combined text

4. Text Chunking (get_text_chunks function):
   - Takes the extracted text as input
   - Creates a RecursiveCharacterTextSplitter with:
     - Chunk size of 10,000 characters
     - Overlap of 1,000 characters between chunks
   - Splits the input text into chunks
   - Returns the list of text chunks

5. Vector Store Creation (get_vector_store function):
   - Takes text chunks as input
   - Creates embeddings using GoogleGenerativeAIEmbeddings
   - Initializes a FAISS vector store with the text chunks and embeddings
   - Saves the vector store locally as "faiss_index"

6. Conversational Chain Setup (get_conversational_chain function):
   - Defines a prompt template for question answering
   - Initializes a ChatGoogleGenerativeAI model (gemini-pro)
   - Creates a PromptTemplate object with the template
   - Sets up a question-answering chain using the model and prompt
   - Returns the chain

7. User Input Processing (user_input function):
   - Takes a user question as input
   - Loads the previously saved FAISS index
   - Performs a similarity search in the vector store for relevant documents
   - Gets the conversational chain
   - Runs the chain with the relevant documents and user question
   - Prints the response and displays it in the Streamlit interface

8. Main Function:
   - Sets up the Streamlit page configuration
   - Creates a header for the chat interface
   - Sets up a text input for user questions
   - If a question is entered, calls the user_input function
   - Creates a sidebar with:
     - A file uploader for PDF documents
     - A "Submit & Process" button
   - When the button is clicked:
     - Extracts text from the uploaded PDFs
     - Chunks the text
     - Creates and saves a vector store
   - Displays a success message when processing is complete

9. Script Execution:
   - Checks if the script is being run directly
   - If so, calls the main function to start the application
