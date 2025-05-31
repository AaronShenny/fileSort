# AI-Powered File Organizer

An intelligent file organization tool that uses Google's Gemini AI to automatically categorize and organize files based on their content. The script reads various file formats, analyzes their content using AI, and suggests appropriate folder structures for better file management.

## Features

- **Multi-format Support**: Handles PDF, DOCX, CSV, Excel, PowerPoint, images, and text files
- **AI-Powered Categorization**: Uses Google Gemini AI to intelligently categorize files based on content
- **OCR Capability**: Extracts text from images for categorization
- **Interactive Mode**: Asks for user confirmation before moving files
- **Recursive Processing**: Processes all files in subdirectories
- **Error Handling**: Robust error handling for various file types and edge cases

## Supported File Formats

| Format | Extensions | Method |
|--------|------------|--------|
| PDF | `.pdf` | PyMuPDF text extraction |
| Word Documents | `.docx` | python-docx |
| Spreadsheets | `.csv`, `.xls`, `.xlsx` | pandas |
| Presentations | `.pptx` | python-pptx |
| Images | `.jpg`, `.jpeg`, `.png`, `.bmp`, `.tiff` | OCR with Tesseract |
| Text Files | `.txt`, `.py`, `.json`, `.html`, `.xml`, `.md` | Direct text reading |

## Prerequisites

### Python Packages
```bash
pip install PyMuPDF python-docx pandas python-pptx Pillow pytesseract google-genai
```

### System Dependencies
- **Tesseract OCR**: Required for image text extraction
  - **Ubuntu/Debian**: `sudo apt-get install tesseract-ocr`
  - **macOS**: `brew install tesseract`
  - **Windows**: Download from [GitHub releases](https://github.com/UB-Mannheim/tesseract/wiki)

### API Setup
1. Get a Google AI Studio API key from [Google AI Studio](https://aistudio.google.com/)
2. Replace the API key in the script:
   ```python
   client = genai.Client(api_key='YOUR_API_KEY_HERE')
   ```

## Installation

1. Clone or download the script
2. Install required packages:
   ```bash
   pip install -r requirements.txt
   ```
3. Install Tesseract OCR (see prerequisites)
4. Configure your Google AI API key

## Usage

1. Run the script:
   ```bash
   python file_organizer.py
   ```

2. Enter the root folder path when prompted:
   ```
   Enter the root folder path: /path/to/your/files
   ```

3. The script will:
   - Process each file in the directory
   - Extract content based on file type
   - Send content to Gemini AI for categorization
   - Suggest a folder name/category
   - Ask for your approval before moving files

4. For each file, you'll see:
   ```
   📂 Processing: /path/to/file.pdf
   ✅ Gemini Output: {"content": "...", "label": "Research Papers", "filename": "file.pdf"}
   📝 Suggested move: file.pdf → Research Papers/
   Do you want to move this file? [y/N]:
   ```

## How It Works

1. **File Discovery**: Recursively scans the specified directory
2. **Content Extraction**: Uses format-specific readers to extract text content
3. **AI Analysis**: Sends content to Google Gemini AI with structured output requirements
4. **Categorization**: AI returns a JSON response with suggested label/category
5. **Organization**: Creates folders and moves files based on AI suggestions (with user approval)

## AI Response Schema

The script expects Gemini to return JSON with this structure:
```json
{
  "content": "Brief summary of file content",
  "label": "Suggested folder name",
  "filename": "Original filename"
}
```

## Safety Features

- **User Confirmation**: Always asks before moving files
- **Duplicate Handling**: Skips files already in correct folders
- **Error Recovery**: Continues processing even if individual files fail
- **Path Validation**: Checks if directories exist before processing

## Configuration Options

You can modify the script to:
- Change the AI model: `model = "gemini-2.5-flash-preview-05-20"`
- Adjust response schema for different categorization needs
- Add support for additional file formats
- Customize the prompt sent to the AI

## Error Handling

The script handles various error scenarios:
- Unreadable files
- API failures
- File permission issues
- Network connectivity problems
- Unsupported file formats

## Limitations

- Requires active internet connection for AI processing
- API usage costs may apply based on Google AI pricing
- OCR accuracy depends on image quality
- Processing time varies based on file size and content

## Contributing

Feel free to contribute by:
- Adding support for new file formats
- Improving error handling
- Enhancing the AI prompts
- Adding configuration options

## License

MIT License

## Troubleshooting

### Common Issues

1. **Tesseract not found**: Ensure Tesseract is installed and in your PATH
2. **API errors**: Check your API key and internet connection
3. **Permission denied**: Ensure the script has read/write access to target directories
4. **Import errors**: Install all required packages using pip

### Debug Mode

Add debug prints by modifying the error handling sections to get more detailed error information.
