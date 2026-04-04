# Exploring Docling Open Source Basics

  * Tool name: Docling
  * Language used: Python
  * Organization: Fedora Project : March - April 2026 Outreachy Contribution

## Introduction
### What is Docling
Docling is an open-source document processing tool used to parse, convert, and structure content from documents such as PDFs into machine-readable formats like Markdown, HTML, YAML, and JSON and is commonly used in AI pipelines, such as Retrieval Augmented Generation (RAG), to prepare documents for downstream analysis and retrieval tasks.

### What is Docling CLI
Docling CLI is the command-line tool used to run Docling functions such as document conversion, format selection, and pipeline testing directly from  terminal.

## Objective
The objective of this task is to explore the basic functionality of Docling as an open-source document processing tool;

* Install Docling
* Verify installation
* Convert PDF documents
* Test different output formats
* Compare CLI options
* Analyse results

  1. ## Install Docling
Before installing Docling, I prepared a project workspace by navigating to the project directory, verifying the Python version, creating and activating a virtual environment, and organizing folders which are; data, outputs, and screenshots. This setup ensured a clean development environment and proper project structure:

      * Move to Desktop
     Move to where the project folder is located
                cd Desktop/

      * Navigate to outreachy folder
      Navigate to main project directory created for Outreachy tasks.
                cd outreachy/

      * Navigate to docling project folder
      Move into the specific project directory where Docling exploration work is done.
                 cd docling

      * Check Python version
      Confirmed Python is installed and checked compatibility (Docling requires Python 3.9+ typically)
      
                 python --version

      * Create virtual environment
      Created an isolated Python environment named my_doc to avoid dependency conflicts.
      
                 python -m venv my_doc

      * Activate virtual environment
      Activated the virtual environment so packages install locally instead of globally.
      Everytime I use docling I activate virtual environment to find docling
      
                 source my_doc/Scripts/activate

       * Created folders
       Created a directory to store terminal and output screenshots for documentation
                 mkdir screenshots

       Created folder to store input files/PDFs
                 mkdir data

       Created folder to store converted files Markdown, HTML, JSON, YAML, outputs.
                 mkdir outputs

       Displayed the created project structure
                 ls

      

  2. ## Verify installation
  3. ## Convert PDF documents
  4. ## Test different output formats
  5. ## Compare CLI options
  6. ## Analyse results
