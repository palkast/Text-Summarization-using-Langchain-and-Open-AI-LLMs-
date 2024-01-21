# Text-Summarization-using-Langchain-and-Open-AI-LLMs-
This project is created to show different techniques of text summarization from pdf/text using Open AI LLM models.

# Techniques :

# A)Basic Prompt Summarization

1.Try to import open AI langchain chat models.
2.There are 3 kinds of messages that we would lik to define. Try to define chat messages.
*AI message* - response from llm models 
*Human message* - is message from human input 
*System message* - is the initial message for the AI system to behave as eg. act like a poet
3.Get the response back from llm model by calling llm model with chat_messages.

# B)Prompt Templates Text Summarization

1.To create own custom prompt template and get response from LLM model.
2.Prompt template can have multiple prompts so use * llmchain * from langchain.chains
3.Create a generic template 
4.Create prompt template using input variables speech and language 
5.Save to complete prompt 
6.Run llmchain 

# C)StuffDocumentChain Text Summarization

1.Get the entire doc give it to llm to summarize.
2.Read pdf using pypdf which creates a pdf object reader .
3.Enumerte through every page and extract text in text 
4.Give entire text to llm model 
5.Convert text to documents
from langchain.docstore.document import Document
initialize prompttemplate , 
load_summarize_chain : mention chain_type = stuff 
chain = load_summarize_chain(
    llm,
    chain_type='stuff',
    prompt=prompt,
    verbose=False
)
6.Ai understands now this is a chain , waiting for a doc then call llm and get llm response.

# D)Summarizing Large Documents Using Map Reduce

1.When we have huge data of 1 gb /2 gb and there is restriction of token so we have to use map reduce. 
2.divide pdf into chunks , for every chunk get a summary 
3.finally llmmodel will take all the summaries and generate a final summary 
4.how to divide document into chunks using from langchain.text_splitter import RecursiveCharacterTextSplitter
5.Mention chain_type is map reduce 
chain = load_summarize_chain(
    llm,
    chain_type='map_reduce',
    verbose=False
)
summary = chain.run(chunks)

# E)Map Reduce With Custom Prompts

1.while giving chunks to llm model we can do lots of things to customize the prompt 
chunks_prompt="""
Please summarize the below speech:
Speech:`{text}'
Summary:
"""
map_prompt_template=PromptTemplate(input_variables=['text'],
                                    template=chunks_prompt)

final_combine_prompt='''
2.Provide a final summary of the entire speech with these important points.
3.Add a Generic Motivational Title,
4.Start the precise summary with an introduction and provide the summary in number points for the speech.
Speech: `{text}`
'''
final_combine_prompt_template=PromptTemplate(input_variables=['text'],
                                             template=final_combine_prompt)


# F)RefineChain For Summarization

1.Take first chunk give a summary.
2.For second chunk combine chunk1 and chunk2 we give it to LLM model and we get a summarized version.
3.In 3rd we combine chunk 1, 2,3 and combine them and give it to llm to get text summarized version.
4.Do this till end to get final output summary





