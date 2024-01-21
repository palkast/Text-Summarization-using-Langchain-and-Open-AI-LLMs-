# Text-Summarization-using-Langchain-and-Open-AI-LLMs-
This project is created to show different techniques of text summarization from pdf/text using Open AI LLM models.<br />
In this project I have tried to read a *pdf* from **Mayo Clinic(US No.1 Hospital and Research)** guidelines and summarized it.<br />

# Techniques :

# A)Basic Prompt Summarization

1.Try to import open AI langchain chat models.<br />
2.There are 3 kinds of messages that we would lik to define. Try to define chat messages.<br />
*AI message* - response from llm models<br /> 
*Human message* - is message from human input<br /> 
*System message* - is the initial message for the AI system to behave as eg. act like a poet<br />
3.Get the response back from llm model by calling llm model with chat_messages.<br />

# B)Prompt Templates Text Summarization

1.To create own custom prompt template and get response from LLM model.<br />
2.Prompt template can have multiple prompts so use * llmchain * from langchain.chains<br />
3.Create a generic template<br /> 
4.Create prompt template using input variables speech and language<br /> 
5.Save to complete prompt<br /> 
6.Run llmchain<br /> 

# C)StuffDocumentChain Text Summarization

1.Get the entire doc give it to llm to summarize.<br />
2.Read pdf using pypdf which creates a pdf object reader.<br />
3.Enumerte through every page and extract text in text.<br /> 
4.Give entire text to llm model.<br />
5.Convert text to documents.<br />
from langchain.docstore.document import Document
initialize prompttemplate , 
load_summarize_chain : mention chain_type = stuff 
chain = load_summarize_chain(
    llm,
    chain_type='stuff',
    prompt=prompt,
    verbose=False
)
6.Ai understands now this is a chain , waiting for a doc then call llm and get llm response.<br />

**Please check the summarized output from Mayoclinic.pdf :**<br />

[![Mayo-Clinic-Screenshot-2024-01-21-123904.png](https://i.postimg.cc/kMy1f93s/Mayo-Clinic-Screenshot-2024-01-21-123904.png)](https://postimg.cc/NL5kj302)

# D)Summarizing Large Documents Using Map Reduce

1.When we have huge data of 1 gb /2 gb and there is restriction of token so we have to use map reduce.<br /> 
2.Divide pdf into chunks , for every chunk get a summary.<br />
3.Finally llmmodel will take all the summaries and generate a final summary.<br /> 
4.Now will check how to divide document into chunks using from langchain.text_splitter import RecursiveCharacterTextSplitter<br />
5.Mention chain_type is map reduce<br />
chain = load_summarize_chain(
    llm,
    chain_type='map_reduce',
    verbose=False
)
summary = chain.run(chunks)

# E)Map Reduce With Custom Prompts

1.While giving chunks to llm model we can do lots of things to customize the prompt<br /> 
chunks_prompt="""
Please summarize the below speech:
Speech:`{text}'
Summary:
"""
map_prompt_template=PromptTemplate(input_variables=['text'],
                                    template=chunks_prompt)

final_combine_prompt='''
2.Provide a final summary of the entire speech with these important points.<br />
3.Add a Generic Motivational Title<br />
4.Start the precise summary with an introduction and provide the summary in number points for the speech.<br />
Speech: `{text}`
'''.
final_combine_prompt_template=PromptTemplate(input_variables=['text'],
                                             template=final_combine_prompt)


# F)RefineChain For Summarization

1.Take first chunk give a summary.<br />
2.For second chunk combine chunk1 and chunk2 we give it to LLM model and we get a summarized version.<br />
3.In 3rd we combine chunk 1, 2,3 and combine them and give it to llm to get text summarized version.<br />
4.Do this till end to get final output summary.<br />





