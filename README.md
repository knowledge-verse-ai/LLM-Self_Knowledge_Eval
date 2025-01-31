# Line of Duty: Evaluating LLM Self-Knowledge via Consistency in Feasibility Boundaries

## Abstract

As LLMs grow more powerful, their most profound achievement may be recognising when to say "I don't know". Existing studies on LLM self-knowledge have been largely constrained by human-defined notions of feasibility, often neglecting the reasons behind unanswerability by LLMs and failing to study deficient types of self-knowledge. This study aims to obtain intrinsic insights into different types of LLM self-knowledge with a novel methodology: allowing them the flexibility to set their own feasibility boundaries and then analysing the consistency of these limits. We find that even frontier models like GPT-4o and Mistral Large cannot accurately judge their own capabilities more than 80\% of the time, highlighting a significant lack of trustworthiness in responses. Our analysis of confidence balance in LLMs indicates that models swing between overconfidence and conservatism in feasibility boundaries depending on task categories and that the most significant self-knowledge weaknesses lie in temporal awareness and contextual understanding. These difficulties in contextual comprehension additionally lead models to question their operational boundaries, resulting in considerable confusion within the self-knowledge of LLMs. 

<p align=center><img width=800pt  src="https://github.com/user-attachments/assets/52dc1cab-924f-4438-a024-2958db6fefd5"></p>
<br>
<p align=center><em>Overview of our methodology depicting key steps</em></p>


## Implementation Setup
This codebase allows you to **generate** and **classify** both feasible and infeasible tasks using different AI models.  
It provides two main commands:  
1. `generate` - Generates feasible/infeasible tasks based on specified parameters.  
2. `classify` - Classifies tasks from the generated file.  

Ensure you have Python installed (version 3.10+ recommended).  

1. **Clone the repository or place the script in a directory**

2. **Navigate to the script's directory**  
   ```sh
   cd /path/to/script
   ```
   
3. **Install dependencies and requirements**
   ```
   pip install -r requirements.txt
   ```  
4. **Run the script with the appropriate command and options as given below in the usage guide.**  

---

## **Usage Guide**

### **1. Generating Tasks**
The `generate` command creates tasks based on specified parameters.  

#### **Command Structure:**
```sh
python main.py generate --model <MODEL> --type_of_self_knowledge <SELF_KNOWLEDGE> --type_of_task <TASK_TYPE> --prompt_type <PROMPT_TYPE> --number_of_tasks <NUMBER>
```

#### **Required Arguments:**
| Argument                  | Description                                                                                     | Allowed Values |
|---------------------------|-------------------------------------------------------------------------------------------------|---------------|
| `--model`                 | AI model to use for task generation.                                                           | `'gpt-4o-mini', 'gpt-4o', 'gemini-1.5-flash', 'claude-3-5-sonnet-latest', 'mistral-large-latest'` |
| `--type_of_self_knowledge` | Type of self-knowledge to focus on.                                                            | `'Capability Boundary', 'Contextual Awareness', 'Identification of Ambiguity', 'Ethical Integrity', 'Temporal Perception'` |
| `--type_of_task`          | Type of task to generate.                                                                      | `'feasible', 'infeasible'` |
| `--prompt_type`           | Type of prompt to use.                                                                        | `'vanilla', 'challenge_qap'` |
| `--number_of_tasks`       | Number of tasks to generate.                                                                  | Integer (e.g., `5`, `10`, etc.) |

#### **Example Usage:**
```sh
python script.py generate --model gpt-4o --type_of_self_knowledge "Contextual Awareness" --type_of_task feasible --prompt_type vanilla --number_of_tasks 5
```
This command generates **5 feasible tasks** using **GPT-4o**, with a focus on **Contextual Awareness** and a **vanilla prompt**.

---

### **2. Classifying Tasks**
The `classify` command analyzes and categorizes tasks from a file.  

#### **Command Structure:**
```sh
python main.py classify --model <MODEL> --file_path <FILE_PATH> --prompt_type <PROMPT_TYPE>
```

#### **Required Arguments:**
| Argument       | Description                                    | Allowed Values |
|---------------|------------------------------------------------|---------------|
| `--model`     | AI model to use for classification.            | `'gpt-4o-mini', 'gpt-4o', 'gemini-1.5-flash', 'claude-3-5-sonnet-latest', 'mistral-large-latest'` |
| `--file_path` | Path to the file containing tasks to classify. | Excel (.xlsx) file path only, in the format generated above |
| `--prompt_type` | Type of prompt to use.                      | `'vanilla', 'challenge_qap'` |

#### **Example Usage:**
```sh
python script.py classify --model gemini-1.5-flash --file_path "generation_results\gemini-1.5-flash_results.xlsx" --prompt_type challenge_qap
```
This command classifies tasks from `"generation_results\gemini-1.5-flash_results.xlsx"` using **Gemini-1.5-Flash** with a **challenge_qap prompt**.

---

## **Error Handling & Notes**
- Ensure all required arguments are provided; missing arguments will result in an error.  
- If using spaces in values (e.g., `"Contextual Awareness"`), wrap them in quotes (`""`).  
- Supported file format for classification is only **Excel (.xlsx)** generated using the **generate** option.  



