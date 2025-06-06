# Section 10. LLMs for Chemistry

- **Brief Introduction ✅**
    
    Large Language Models, or LLMs, are advanced machine learning models capable of understanding and generating human-like text and answering QA questions based on extensive training data from diverse sources.
    
    In chemistry, these models assist researchers and students by automating information retrieval, predicting chemical reactions, and supporting molecular design tasks. Benchmarks such as ChemLLMBench provide datasets to evaluate the accuracy and reliability of LLMs in chemical contexts.
    
    So what exactly are LLMs and why are they so powerful?  We will dive into this in this section.
    
- **10.1 Introduction of LLMs✅**
    
    **What are LLMs?**
    
    - Large Language Models (LLMs) are smart computer systems like ChatGPT and Gemini. They learn from huge amounts of text data and can understand and generate human-like writing.
    
    **What can they do?**
    
    - These AI models can understand the meaning behind words, answer questions, and even come up with new ideas.
    - In chemistry, LLMs are helpful because they can:
        - Simplify complicated chemical information.
        - Make difficult tasks easier to handle.
        - Quickly find and organize important data.
        - Help automate tasks that might otherwise take scientists a long time to complete.
        - Summarizing extensive research articles or reports succinctly.
    
    In short, LLMs help make complex information clearer and easier to work with, even if you don't have a chemistry background. 
    
    → Such applications can substantially speed up research processes, improve accuracy, and open new avenues for innovative scientific discoveries.
    
- **10.2 Prompt Engineering⌛**
    
    **Definition:**
    Prompt engineering involves carefully writing instructions (prompts) to guide Large Language Models (LLMs) to give accurate and useful answers. In simpler terms, it's how you ask questions or provide information to an AI system clearly and specifically.
    
    **Why is it important in chemistry?**
    Chemists often ask AI models to help with complex tasks, such as predicting chemical reactions or interpreting experimental data. Clear and detailed prompts help the AI understand exactly what information you're looking for
    
    - **Format of a Good Prompt:**
    A well-structured prompt typically contains these key parts:
        - **General Instruction:** Briefly describes the task context or role the model is expected to perform.
            - Example: *"You are an expert chemist. Given the [***Specific Task***], your task it to predict [***Specific Task***] using your chemical knowledge [of the specific task] to get the correct answer.[***Input Explanation** *].[***Output Explanation and Restriction***].[***Few shot prompt***]"*
        - **Specific Task:** Clearly states exactly what you want the model to do.
            - Example: *"Predict the product of a chemical reaction. "*
        - **Input Explanation:** Specifies the data or information provided.
            - Example: *"Given the reactants aspirin and hydrochloric acid..."*
        - **Output Explanation and Restrictions:** Clearly describes the format and type of response desired, with any limitations.
            - Example: *"Provide the reaction products in SMILES notation only, without additional explanations."*
        - **Few shot prompt:** Few-shot prompting involves providing examples of similar problems and solutions within your prompt. This helps the model understand precisely what is expected by learning from these given examples.
            - **Example of Few-shot Prompt:**
                - Input: *"Reactants: aspirin + hydrochloric acid. Products (SMILES): xxxx"*
                - Output: *"[Exact product SMILES]"*
                - Input: *"Reactants: benzene + nitric acid. Products (SMILES): xxxx"*
                - Output: *"[Exact product SMILES]"*
    
    **Example of Prompt Engineering:**
    
    *Task: Analyze the interaction between hydrogen gas and water.*
    
    "You are an expert in chemist. I am exploring basic chemical interactions and need a detailed explanation of what happens when hydrogen gas (H₂) is introduced to water (H₂O) under standard conditions. Using your experienced chemical  knowledge please describe:
    
    - The physical and chemical properties of hydrogen in water,
    - Any possible reactions or interactions (if any) between hydrogen and water,
    - The conditions under which a reaction might occur,
    - Potential energy changes or hazards involved, and
    - Why the reaction does or does not proceed under normal conditions.
    
    Provide clear explanations and any relevant safety considerations."
    
    - **Tips for effective prompt engineering:**
        - **Clarity:** Always be specific and clear.
        - **Context:** Provide important details like chemical names, reaction conditions, or experimental setup.
        - **Structured Requests:** Clearly state what kind of response you expect (e.g., chemical structure, explanation, prediction).
        - **Examples:** Sometimes providing examples (known as few-shot prompting) can help the model understand the desired answer format better.
- **10.3 LLMs Call for Tools⌛**
    
    → organize later  →  Could be an agent to acquire external information
    
    ### **Definition**
    
    In addition to text-based interactions, LLMs can call and integrate specialized chemistry databases and computational chemistry tools. Chemists can configure LLMs to directly interact with these external resources to achieve more precise and sophisticated analyses, such as:
    
    - **Chemical data extraction:** Utilizing ChemSpider, PubChem, or Chemical Abstracts Service (CAS) to retrieve precise compound details.
    - **Molecular property predictions:** Leveraging computational chemistry tools like RDKit or Cheminformatics software for predicting physical and chemical properties.
    - **Reaction prediction and retrosynthesis:** Employing retrosynthesis tools and computational chemistry simulations to predict feasible reaction pathways or syntheses.
    
    ⇒ This integration reduces human error, accelerates research, and increases the depth of chemical insights generated.
    
    ### **Chemistry-specific Tools**
    
    - **RDKit:** Comprehensive description, capabilities (visualization, molecular validation, structure prediction), and practical installation and usage instructions.
    - **Chemical Databases (PubChem, ChemSpider):** Guide on querying chemical data through APIs.
    - **ChemBench:** A platform for benchmarking LLMs in chemistry.
    
    ### Example Code:  **Validating Generated Molecule**
    
    ```python
    from rdkit import Chem
    smiles = "C1=CC=CC=C1"  # Benzene SMILES
    molecule = Chem.MolFromSmiles(smiles)
    if molecule:
        print("Valid molecule!")
    else:
        print("Invalid molecule.")
    
    ```
    
- **10.4 Usage of LLM APIs⌛**
    
    → How to evaluate performance, calculate the matrix of the dataset → how well can it done. Ask for user input 0 or 1  
    
    Chemists can utilize APIs provided by popular LLM platforms such as OpenAI, Google, and other AI providers. Using APIs, chemists can:
    
    - Embed intelligent text-based query capabilities directly into their chemical informatics software or laboratory information management systems.
    - Automate literature review tasks, identifying relevant publications, extracting pertinent data, and summarizing extensive research quickly and accurately.
    - Create custom interfaces or dashboards where chemical data can be analyzed interactively by leveraging AI-generated insights from LLM APIs.
    
    For example, OpenAI provides straightforward documentation to help developers and chemists implement their APIs into software, facilitating rapid adoption.
    
    ### **Setting Up OpenAI API**
    
    1. Install the OpenAI Python library:
        
        pip install openai
        
        Add API to the environment file or secret book if you are using google colab
        
    2. Python Example: Basic Chemical Information Query
    
    ```python
    from openai import OpenAI
    # Creat model
    client = OpenAI()
    # Function to call when you want to ask something
    completion = client.chat.completions.create(
        model="gpt-4o-mini",
        messages=[
            {"role": "system", "content": "You are a helpful assistant. Response in Markdown format"},
            {
                "role": "user",
                "content": [{"type":"text","text": "What is the element silver in the chemistry"}]
            }
        ],
    )
    ```
    
    ### Loading the dataset
    
    First import the file of dataset into the environment 
    
    Then run this code
    
    ```python
    import pandas as pd
    
    # Load CSV file
    df = pd.read_csv("dataset.csv")
    
    # Display first few rows
    print(df.head())
    
    ```
    
- **10.5 Interactive Programming⌛**
    
    →introduce code more effectively like copilot
    
    → using llms to code effectively and better. Use it to debug, help with code
    
    ### Definition
    
    Interactive programming involves developing code incrementally, with immediate feedback, typically using environments like Jupyter Notebooks or Google Colab.
    
    ### Set up the environment using Google Colab
    
    1. Add the API to the ***Secret :***
        1. Look over to the left bar → choose the key icon (secrets)
        2. Choosing Add new secrets → fill in the name of the API (we might call this in the future so an intuitive name would be easier for future handling) and the value with the API
        3. Tick notebook access 
    2. Choosing the code on the top bar at the top
    
    ```python
    # Install OpenAI library
    !pip install --q openai
    ```
    
    ```python
    from openai import OpenAI
    import pandas as pd
    
    # Creat model
    client = OpenAI()
    # Function to call when you want to ask something
    def gpt_set_up(prompt, file_path=None):
      data_info = ""
      if file_path:
        if file_path.endswith(".csv"):
            df = pd.read_csv(file_path)
            data_info = f"\nHere is a summary of the provided dataset:\n{df.head().to_string()}\n"
      message = [
              {"role": "system", "content": "You are a helpful assistant. Response in Markdown format"},
              {
                  "role": "user",
                  "content": [{"type":"text","text": prompt}]
              }
      ]
      if data_info:
          message.append({"role": "user", "content": [{"type": "text", "text": data_info}]})
      completion = client.chat.completions.create(
          model="gpt-4o-mini",
          messages= message,
          #Control the length of the answer and get the top answer
          temperature=1,
          max_tokens=1000,
          top_p =1,
      )
      return completion.choices[0].message.content.strip()
    
    ```
    
    ```python
    from IPython.display import Markdown, display
    # Calling the function to ask question
    output = gpt_set_up(prompt=input("Enter a prompt: "))
    display(Markdown(output))
    
    ```
    
    Example Link: [https://colab.research.google.com/drive/1B8qFtN_mkEzX3BGaznvXIstn0P1w6yRP?usp=sharing](https://colab.research.google.com/drive/1B8qFtN_mkEzX3BGaznvXIstn0P1w6yRP?usp=sharing)
    
    ⇒By understanding and applying these concepts effectively, chemistry students and researchers can fully harness the transformative potential of LLMs, pushing the boundaries of chemical research and innovation. 
    
    ⇒Moreover, future advancements could involve autonomous AI agents capable of independently exploring, studying, and retrieving chemical information in real time. Such autonomous systems, which learn dynamically and gather relevant data on demand rather than relying solely on static pre-trained datasets, could significantly enhance the accuracy, timeliness, and adaptability of chemical research. 
    
    ⇒Enabling AI to autonomously explore databases, perform analyses, and synthesize new knowledge dynamically would represent a substantial step forward, empowering chemists to tackle increasingly complex scientific challenges with unprecedented efficiency and innovation.