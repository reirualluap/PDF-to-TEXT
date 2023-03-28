# PDF-to-TEXT [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/reirualluap/PDF-to-TEXT/blob/main/pdf_to_text.ipynb])
Transform any .pdf to an .txt file in a few second

# Require : 
!pip install PyPDF2

!pip install regex

# Use : 

1 - Select your .pdf file via an files.upload()

2 - PyPDF2 extract text and use regex to reform the whole text

3 - Download the output via an files.download()

# CODE 

```
import PyPDF2 
import re
from google.colab import files

uploaded = files.upload()

def extract_text_from_pdf(pdf_file: str) -> [str]:
    with open(pdf_file, 'rb') as pdf:
        reader = PyPDF2.PdfReader(pdf)
        pdf_text = []
        for page in reader.pages:
            content = page.extract_text()
            pdf_text.append(content)
        return pdf_text

def split_message(text: str) -> [str]:
    return text.split()

def main():
    pdf_file = list(uploaded.keys())[0]
    extracted_text = extract_text_from_pdf(pdf_file)
    pdf_filename = pdf_file.split('.')[0]

    text_file_path = f"{pdf_filename}.txt"

    with open(text_file_path, "w", encoding="utf-8") as text_file:
        for text in extracted_text:
            split_message_list = split_message(text)
            text_file.write(' '.join(split_message_list))
            text_file.write("\n")

        up_text_file_path = files.download(text_file_path)    
    return up_text_file_path

if __name__ == "__main__":
    main()

```
