# Building Reproducible LLM Applications 1: Structured Generation

1. What is Structured Generation?
    1. Introduction
        1. Language models have great promise but are considered unpredictable
        2. How to move from invocations to programs
    2. Definition
        1. Structured generation is a paradigm for controlling language models by specifying input-output transformations
    3. Objectives
        1. Not to create an autonomous agent
        2. To compose complex systems into multiple reliable steps
        3. Each step is an explicit structured transformation: `InputType --> OutputType`
    4. Concepts
        1. Language models as dynamical systems
        2. Prompting as the traditional way of controlling generation by setting up the dynamical system's initial conditions
    5. User Control
        1. How structured generation gives control to the user
        2. Constraining the space of possible outputs (pruning the transition matrix of the dynamical system)

2. Implementing Structured Generation in Practice
    1. Tool Usage vs JSON Mode
        1. First implementation derived from the concept of tool use
        2. Design pattern for LLM Agents
        3. Allows the agent to choose between outputting raw text or using a tool
    2. Tools
        1. Functions taking raw text as input and outputting structured data
        2. Output can be converted to strings and used as input for the next agent step
        3. Defined with a JSON schema
    3. JSON Schema
        1. Brief explanation of JSON schema
    4. Forced Tool Usage
        1. Equivalent to structured generation
        2. Focus on reliable performance of known computations
    5. Static DAG vs Dynamic DAG
        1. Static DAG: Optimize execution and improve locally
        2. Guarantee of monotonic improvement at the cost of reduced flexibility

3. Defining JSON Schema in Python with Pydantic
    1. Advantages of Pydantic
        1. Human-readable and writable as code
        2. Bridge between LLM generations and Python programs
    2. Features
        1. Defines string-convertible type for each attribute
        2. Includes functional validations and constraints specified as Python functions
    3. Applications
        1. Automatic retries
        2. Error handling
        3. Logging
    4. Prompt Generation
        1. Automatically generate prompts aware of:
            1. Input and output schemas
            2. Python functions that further constrain the output

4. Hands-on Example: Text Classification via Structured Generation
    1. Implementation
        1. Use classification as an example
    2. Evaluation
        1. Evaluate performance based on classification accuracy
    3. Approach
        1. "Graduate student descent" approach to evaluation
        2. Try many things and develop an intuitive internal model
        3. Avoid biases in evaluation

5. Integrating Reasoning in Structured Generation
    1. Approach
        1. Enforce reasoning like ReAct agents or Chain of Thought prompting
        2. Use nested Pydantic models for output
    2. Components
        1. Reasoning Model
            1. Able to follow a sequence of instructions
            2. Reason about the input
        2. Output/Action Model
            1. Generate the final output of the structured generation system
    3. Implementation
        1. Combine components in a nested model
        2. Generate in a single call
        3. Enforce output to be causally influenced by reasoning due to the autoregressive nature of the language model
    4. Evaluation
        1. Assess improvement in accuracy when reasoning is enforced
        2. Discuss the limitations of a simple evaluation framework
        3. Think about what other aspects can be improved or we did not even consider.









# Building Reproducible LLM Applications 2: Scaling Up and Setting Up an Evaluation Framework

1. Introduction
    1. Many Moving parts that can be optimized can influence the quality of the system
        1. LLM provider and hyperparameters (we might be interested in comparing different models each with their own configurations) 
        2. Input Prompt engineering which could include system message, instructions, few shot examples as well as how we explain the model about the schema of the output and the eventual python constraints
        3. Schema of the output and the python constraints that we use to further structure the output
            1. This includes the reasoning schema if we are enforcing reasoning
            2. How we communicate eventual validation failures and handle retries
    2. The more moving parts, the more expensive it is to run enough experiments to have enough statistical confidence about what works and what doesn't
        1. We need to scale our LLM calls to the rate limiting factor
    3. We need to set up an evaluation framework to compare different discrete choices we make without overfitting to our choice history
        1. We use nested cross-validation to avoid these problems
        2. Choices are made in the inner loop and then validated in the outer loop

2. Degrees of Freedom in Structured Generation
    1. LLM Provider
    2. Prompt Engineering
    3. Schema of the output and the python constraints
    4. Reasoning
    5. Error Handling and Retry

3. Scaling Up
    1. Rate Limits (both tokens per minute and requests per minute)
    2. Prefix caching
    3. Storing, saving LLM outputs and resuming for long jobs
    4. Tracking and predicting costs

4. Nested Cross Validation for Discrete Choice Evaluation
    1. We do not have training in our case - we are only concerned with prompt selection
    2. Few shot learning is going to have to be made consistent with train-validation-test
        1. We need to make sure that we are not overfitting nor leaking information across folds
        2. Static vs stochastic validation sets. 
    3. We need to make sure that our evaluation is representative of the real world usage of the system through stratification

5. Interpreting the Results
    1. Performance metrics with unblanced classes
        1. Aggregated metrics: Accuracy, precision, recall, F1-score
        2. Matthews correlation coefficient
    2. Confusion matrix
    3. How to improve the system based on the results


# Building Reproducible LLM Applications 3: Improving the Model

# Building Reproducible LLM Applications 4: Reducing Cost


    

