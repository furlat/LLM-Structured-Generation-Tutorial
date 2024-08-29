1) What is Structured Generation?
    Langauge models have a great promise  but are considered to be unpredictable. How to move from invokations to programs 
    Language models as dynamical systems 
    Prompting as the traditional way of controlling generation by setting up the dynamical system initial conditions 
    how does structured generation give control to the user? by constraining the space of possible outputs (pruning the transition matrix of the dynamical system)
    
2) How is structured generation implemented in practice? Tool usage vs json mode
    First implementation of structured generation is derived from the concept of tool use, which is a design pattern for LLM Agents allowing the agent to choose whether to output raw text or use a tool, that is a function taking raw text as input and outputting structured data.
    that can be converted to string themselves. And used as input for the next agent step. 
    Tools are defined with a Json schema, 
        what is a jsonb schema?
    Forced tool usage ~ structured generation - we are not interested in the agent choosing among possible tools but we want the language model to always use the tool.
3) Defining Jsonschema in python with Pydantic 
    Json schema are a standard way to define data types but are difficult to write and not human readable. 
    We can use Pydantic to define a schema that is human readable and writable as code. It will be a bridge between llm generations and python programs.
4) An hands on example of Text classification via Structured Generation
5) Integrating reasoning in structured generation

