README — Classical Reasoning Agent

Requirements
- Python 3.8+
- Packages: datasets, huggingface_hub
- No generative AI or large language model is used to produce predictions.

How to Run
1. Install the required packages:
   pip install datasets huggingface_hub
2. Open reasoning_agent.ipynb in Jupyter Notebook or JupyterLab.
3. Run all notebook cells in order.
4. The evaluation cell loads RuleTaker, CounterBench, and FOLIO, evaluates the reasoning agent on their public training splits, prints accuracy and inference time, and generates submission.csv.

Public-Dataset Results
Dataset	Accuracy	Correct / Total
RuleTaker	70.04%	336,293 / 480,152
CounterBench	64.50%	645 / 1,000
FOLIO	61.34%	614 / 1,001

Inference time is measured separately for each dataset and printed by the notebook.

Submission Generation
The evaluation cell generates submission.csv containing predictions for the public examples processed by the notebook.

The CSV contains two columns:
- id: Generated identifier using the dataset name and row index.
- predicted_label: Predicted logical label, either True or False.

Note: This CSV contains predictions on public training data. It is not a private-test submission.

Design Summary
- Knowledge representation: Horn-clause-style representation. Each atom consists of a predicate and an argument tuple.
- Variable representation: A term is treated as a variable if it is a single uppercase letter.
- Natural-language parsing: Regex-based templates convert supported sentence structures into symbolic representations. No machine-learning model or LLM is used.
- Reasoning: Unification and forward chaining derive facts. A blocked-fact mechanism supports the implemented counterfactual reasoning cases.
- Generalisation: The system uses symbolic parsing and reasoning rather than memorised dataset IDs or answers. Its performance on unseen inputs depends on the sentence structures and logical patterns supported by the implementation.