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

 ## Environment Set-up 
 The virtual environment was created and activated before installing Docling.
 <p align="center">
<img src="screenshots/environment_setup.JPG" width="700">
</p>

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

## Docling Installation
After successfully seeting up the virtual environment and activated, the next step was to install Docling using pip. This ensures that all required dependencies are installed within the isolated project environment for better reproducibility and dependency management.
 <p align="center">
<img src="screenshots/docling_install.JPG" width="700">
</p>

     pip install docling


  2. ## Verify installation
  After installing Docling, I verified that the installation was successful by checking the installed version:
  Shown in the image above

     docling --version


  3. ## Convert PDF documents

  ## Default PDF conversion
  The first test involved converting a standard PDF (linux.pdf) using the tool's most streamlined approach. Docling CLI default  conversion does not require the user to specify a format in the command. When no flags are provided, Docling automatically defaults to Markdown (.md), which is optimized for structured data extraction
  <p align="center">
 <img src="screenshots/linux_defaulf_options.JPG" width="700">
 </p>

       docling data/linux.pdf
  
  4. ## Test different output formats
  In addition to default conversion(.md format), I used the following commands to convert files and export the source files in the data/ directory to a dedicated outputs/ folder.

  * For a single file conversion I used the command below:
    
                  docling --to html data/linux.pdf --output outputs

       <p align="center">
       <img src="screenshots/single_file_conversion.JPG" width="700">
       </p>

  * For multiple files conversion I used the command below:
  
    - Standard web-based rendering and styling

                  docling --to html data/*.pdf --output outputs

       <p align="center">
       <img src="screenshots/pdf_html.JPG" width="700">
       </p>

    - Programmatic data processing with full metadata
   
                  docling --to json data/*.pdf --output outputs

       <p align="center">
       <img src="screenshots/pdf_json.JPG" width="700">
       </p>

    - Extraction for simple keyword indexing
   
                  docling --to text data/*.pdf --output outputs

      <p align="center">
       <img src="screenshots/pdf_text.JPG" width="700">
       </p>

    - Structural analysis of document elements
   
                  docling --to doctags data/*.pdf --output outputs

       <p align="center">
       <img src="screenshots/pdf_doctags.JPG" width="700">
       </p>

    - Highly readable structured data that is ideal for config-driven pipelines
   
                  docling --to yaml data/*.pdf --output outputs

       <p align="center">
       <img src="screenshots/pdf_yaml.JPG" width="700">
       </p>

    - Web Video Text Tracks; useful for time-aligned or indexed text segments

                  docling --to vtt data/*.pdf --output outputs
        <p align="center">
        <img src="screenshots/pdf_vtt.JPG" width="700">
        </p>

    - Generates separate HTML files for each page, which is critical for memory management in large documents
   
                  docling --to html_split_page data/*.pdf --output outputs

        <p align="center">
        <img src="screenshots/pdf_html_split.JPG" width="700">
        </p>

  
  5. ## Compare CLI options
 
     1. Processing Time

   * The Shortest Processing Time: pdf_md.JPG
      Total Time: 1 minute 50 seconds

      Start Time: 14:25:36

      End Time: 14:27:26

   This command processed data/ folder (3 files) to Markdown. 

  * The Longest Processing Time: pdf_text.JPG
      Total Time: ~9 minutes 04 seconds

       Start Time: 15:23:43
                 
       End Time: 15:32:47
    
      2.              
 


  6. ## Analyse results

     * ## 1. Hardware Resources
Based on the logs on most of my files, my system is relying on local compute power:

Compute Device: The logs explicitly state Using CPU device. My Intel or AMD processor is doing the heavy lifting of "looking" at the PDFs and rebuilding the layout.

AI Models: The model used Torch (PyTorch) as the backend engine. Even though it's on a CPU, it’s loading complex "weights" (770/770 weight files) to ensure high-quality extraction of tables and graphs.

Engine: RapidOCR is being used for text detection. The logs show it's pulling specific models like ch_PP-OCRv4_det_infer.p
     
   * ## Processing Time Analysis

           pdf_md.JPG
       
Markdown is a "low-complexity" format. The tool only needs to identify structure (headers, lists, tables) and write them as plain text. Since Markdown doesn't require heavy metadata wrapping or complex nesting like JSON or HTML, the CPU finishes the "write" phase almost instantly after the OCR is done.

            pdf_text.JPG  sample-tables.pdf
 

 While I expected "text" to be the fastest, the logs reveal a critical bottleneck. 
 
     At 15:28:32, the system hit a   Major Error: std::bad_alloc.
                 
 This is a "Memory Allocation" error. It means the sample-tables.pdf file was likely too complex for your CPU/RAM to handle in this format.
                 
  The system "hung" for several minutes trying to allocate memory before finally failing. The extra 7 minutes in this log weren't spent "converting"—they were spent in a system struggle.

   * ## Storage Space

1. The Storage Hierarchy from Smallest to Largest
Based on the files generated in my outputs/ folder, here is the rank of storage efficiency:

Rank 1: Plain Text (.txt) — Most Efficient

Reasoning: . txt only stores the characters. It strips away all bolding, headers, and table structures. 

Rank 2: Markdown (.md)

Reasoning: .md is similar to text but adds a few extra bytes for symbols like # or | to represent headers and tables. This is usually essential for AI training.

Rank 3: HTML (.html)

Reasoning: .html is significantly heavier than Markdown. For every word, there might be a <div>, <span>, or <p> <img> tag surrounding it.

Rank 4: JSON / YAML — Heaviest Text Format

Reasoning: These are "data-rich." As seen in my output files such aspdf_json.JPG, Docling likely includes the coordinates where on the page the text was and metadata. This can sometimes make a JSON file nearly as large as the original PDF text-stream.
