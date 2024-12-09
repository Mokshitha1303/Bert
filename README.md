# Bert
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Question Answering with BERT-Based Model">
    <meta name="author" content="<Your_Name>">
    <title>Question Answering with BERT</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
            color: #333;
        }
        header {
            background: #333;
            color: #fff;
            padding: 1rem 0;
            text-align: center;
        }
        .container {
            width: 80%;
            margin: auto;
            overflow: hidden;
            padding: 20px;
            background: #fff;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            border-radius: 5px;
        }
        h1, h2, h3 {
            color: #333;
        }
        pre {
            background: #f4f4f9;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            overflow-x: auto;
        }
        code {
            font-family: "Courier New", Courier, monospace;
            color: #d63384;
        }
        a {
            color: #007BFF;
            text-decoration: none;
        }
        a:hover {
            text-decoration: underline;
        }
        footer {
            text-align: center;
            padding: 10px 0;
            margin-top: 20px;
            background: #333;
            color: #fff;
        }
    </style>
</head>
<body>
    <header>
        <h1>Question Answering with BERT-Based Model</h1>
    </header>

    <div class="container">
        <h2>Features</h2>
        <ul>
            <li>Implements a <strong>question-answering pipeline</strong> using a pre-trained model.</li>
            <li>Demonstrates how to use <strong>manual decoding</strong> of model outputs.</li>
            <li>Visualizes the results using <strong>DataFrames</strong>.</li>
        </ul>

        <h2>Prerequisites</h2>
        <p>Ensure you have Python 3.7+ and the following libraries installed:</p>
        <pre><code>pip install torch transformers pandas</code></pre>

        <h2>Code Overview</h2>

        <h3>Import Libraries</h3>
        <pre><code>import torch
import transformers
import pandas as pd
from transformers import AutoModelForQuestionAnswering, AutoTokenizer, pipeline
        </code></pre>

        <h3>Load the Model and Tokenizer</h3>
        <pre><code>model_name = 'deepset/roberta-base-squad2'
model = AutoModelForQuestionAnswering.from_pretrained(model_name)
tokenizer = AutoTokenizer.from_pretrained(model_name)
        </code></pre>

        <h3>Define Input Questions and Contexts</h3>
        <pre><code>QA_input = [
    {'question': 'Why is conversion important?',
     'context': 'The option to convert models between FARM and transformers gives freedom to the user and lets people easily switch between frameworks.'},
    {'question': 'How many programming languages does BLOOM support?',
     'context': 'BLOOM has 176 billion parameters and can generate text in 46 languages and 13 programming languages.'}
]</code></pre>

        <h3>Inference (Manual Decoding)</h3>
        <pre><code># Question 1
inputs0 = tokenizer(QA_input[0]['question'], QA_input[0]['context'], return_tensors="pt")
output0 = model(**inputs0)

answer_start_idx = torch.argmax(output0.start_logits)
answer_end_idx = torch.argmax(output0.end_logits)
answer_tokens = inputs0.input_ids[0, answer_start_idx: answer_end_idx + 1]
answer = tokenizer.decode(answer_tokens)
print(f"Q: {QA_input[0]['question']}\nA: {answer}\n")
        </code></pre>

        <h3>Inference (Pipeline)</h3>
        <pre><code>qa = pipeline('question-answering', model=model_name, tokenizer=model_name)

output_0 = qa(question=QA_input[0]['question'], context=QA_input[0]['context'])
output_1 = qa(question=QA_input[1]['question'], context=QA_input[1]['context'])

print(output_0)
print(output_1)
        </code></pre>

        <h2>Output</h2>
        <h3>Example Questions and Answers:</h3>
        <ul>
            <li><strong>Question:</strong> Why is conversion important?</li>
            <li><strong>Answer:</strong> to convert models between FARM and transformers</li>
        </ul>
        <ul>
            <li><strong>Question:</strong> How many programming languages does BLOOM support?</li>
            <li><strong>Answer:</strong> 13 programming languages</li>
        </ul>

        <h2>Author</h2>
        <p>Developed by <strong>&lt;Your_Name&gt;</strong>. Feel free to reach out for queries or suggestions.</p>

        <h2>License</h2>
        <p>This project is licensed under the MIT License.</p>

        <h2>Contributing</h2>
        <p>Contributions are welcome! Please fork this repository and submit a pull request for any improvements or bug fixes.</p>
    </div>

    <footer>
        <p>&copy; 2024 <Your_Name>. All rights reserved.</p>
    </footer>
</body>
</html>

