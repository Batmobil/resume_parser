# Resume Parser

A robust, LLM-powered tool for extracting structured information from resumes in PDF and Word formats.

## Overview

This project implements a resume parsing system that extracts key information (name, email, and skills) from resume documents. It uses a combination of document conversion techniques and Large Language Models (LLMs) to accurately extract structured data from various resume formats and styles.

## Features

- Supports both PDF and Word (.docx) resume formats
- Extracts candidate's name, email address, and skills
- Handles diverse resume layouts and styles
- Returns structured JSON output
- Robust error handling and validation

## Data and Methodology

The system was developed and tested using a diverse set of 7 synthetic resumes:

- **3 PDF resumes** created using Indeed Resume Builder
- **4 Word (.docx) resumes** created using Microsoft 365 Resume Templates

This approach ensures the parser can handle variations in document structure and is not overfitted to any specific resume style.

## System Design

The resume parsing pipeline follows these steps:

1. **Document Ingestion**: Accept resumes in PDF or Word (.docx) format
2. **Document-to-Markdown Conversion**: Convert documents to standardized Markdown format
3. **LLM-based Information Extraction**: Process the Markdown text with a carefully crafted prompt
4. **Structured Output Generation**: Return extracted information in JSON format
5. **Output Validation**: Validate the output against a defined schema

## Technical Stack

- **Document Conversion**: 
  - `markitdown` for converting both PDF and Word documents to Markdown
  
- **LLM Integration**:
  - OpenRouter API for accessing LLM capabilities
  - Default model: `gpt-4.1-mini` (balancing cost and performance)
  
- **Data Validation**:
  - `pydantic` for schema definition and validation
  
- **Environment Management**:
  - `uv` for dependency management

## Implementation Details

The core of the implementation is the `ResumeParser` class, which:

1. Converts the input document to Markdown format
2. Sends the Markdown content to an LLM with a specialized prompt
3. Processes the LLM response and validates it against a Pydantic model
4. Returns a structured JSON object with the extracted information

The system uses prompt engineering techniques to handle edge cases such as:
- Extracting suite names (e.g., "Microsoft Office") rather than individual products
- Including generic skills like "Communication" or "Problem-solving"
- Excluding languages from the skills list


## Testing and Evaluation

The system was tested against 7 diverse resume samples (4 Word, 3 PDF) with a pragmatic testing approach using assert-based validation. All test cases passed successfully, demonstrating the parser's ability to handle different document formats and resume styles.

## Future Improvements

For a production-grade solution, consider:

1. **Formal Testing Framework**: Implement a comprehensive test suite using `pytest`
2. **Skills Standardization**: Develop a formal taxonomy or ontology for skills
3. **Additional Fields**: Extend extraction to include work experience, education, etc.
4. **Performance Optimization**: Implement caching and batch processing for efficiency
5. **UI/API Development**: Create a user interface or API for easier integration

## Installation and Usage

```python
# Example usage
from resume_parser import ResumeParser

# Initialize the parser
parser = ResumeParser()

# Parse a resume
result = parser("path/to/resume.pdf")
# Or
result = parser("path/to/resume.docx")

# Access the extracted information
print(f"Name: {result['name']}")
print(f"Email: {result['email']}")
print(f"Skills: {', '.join(result['skills'])}")
```

## Requirements

- Python 3.12+
- Dependencies listed in `pyproject.toml`
- OpenRouter API key (set as environment variable `API_KEY`)

## Development Approach

This project follows a **Test-Driven Development (TDD)** approach:

1. Tests were written first to define the expected behavior
2. Implementation was developed to satisfy these tests
3. The code was refactored while maintaining test compliance

This methodology ensures that the parser correctly handles the required inputs and produces the desired structured output, serving as a development roadmap throughout the project.

## Conclusion

This resume parser demonstrates how modern NLP techniques, particularly LLMs, can be leveraged to extract structured information from unstructured documents. By combining document conversion tools with carefully crafted prompts, the system achieves high accuracy in extracting key information from diverse resume formats and styles.

The project serves as a proof of concept that can be extended into a production-ready solution with additional features and optimizations.
