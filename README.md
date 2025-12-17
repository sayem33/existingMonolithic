# LLM-Powered Online Teaching Assistant for Requirements Engineering (RE) Course (APUOPE-RE)

## Latest Architecture Update (December 2025)

### Unified GPT-4o Implementation
- **All Tasks**: Now use GPT-4o for consistent performance across:
  - Summarization (short/detailed summaries)
  - Conceptual Q&A (conceptual questions)
  - Application Q&A (application-based questions)
  - Quiz Generation (MCQ/true-false questions)
- **LLM-as-Judge Evaluation**: GPT-4o for content quality assessment
- **Evaluation Metrics**: LLM-as-Judge + Automated Metrics (Word-F1, Length Ratio)

### Benchmark Testing Framework
- **90-test Dataset**: Comprehensive evaluation of Requirements Engineering content
- **Task Types**: 4 categories with automated quality scoring
- **Performance Metrics**: Latency, success rates, quality scores (0-10 scale)

## Live Project Link
[https://comp-se-610-620-autumn-2024-software.onrender.com/](https://comp-se-610-620-autumn-2024-software.onrender.com/)

## User Acceptance Testing (UAT) Process

### Step-1: Register as a Teacher and Login as a Teacher

1. **Register and Login**
   - Register with any email and set a password.
   - Choose 'teacher' from the role panel.
   - Login after completing the registration.

2. **Dashboard**
   - Navigate to the Dashboard to see an overview of the course with progress.
   - Note: This page is structured with dummy data and is not integrated with live data as it was not required by the customer. Further development is planned.

3. **Materials**
   - If any material is listed, delete them for a fresh start.
   - Add your own materials. Materials can be any PDF file on your PC.

4. **Studying Lectures**
   - View uploaded materials in the list panel.
   - Choose any material from the list and use the following buttons:
     - "Generate Conceptual Example" (GPT-4o powered)
     - "Generate Summary" (GPT-4o powered short/detailed summaries)
     - "Find Contents" (GPT-4o powered content analysis)
   - All generation uses GPT-4o for high-quality, consistent responses
   - After generating the response, check the relevance of the content using the "Check Relevance" button (this button appears after generating a response).
   - Write prompts in the text field below for further analysis on the material.

5. **Quiz**
   - No information will be displayed initially as no student has taken any quiz yet.

6. **Assignment**
   - No information will be displayed initially as no student has submitted any assignment yet.

7. **Feedback**
   - No information will be displayed initially as no student has submitted any feedback yet.

### Step-2: Register as a Student and Login as a Student

1. **Register and Login**
   - Register with another email and set a password.
   - Choose 'student' from the role panel.
   - Provide any ID as the student ID.
   - Login after completing the registration.

2. **Dashboard**
   - Navigate to the Dashboard to see an overview of the course with progress.
   - Note: This page is structured with dummy data and is not integrated with live data as it was not required by the customer. Further development is planned.

3. **Materials**
   - View materials uploaded by the teacher.
   - As a student, you can only view materials uploaded by the teacher. You cannot upload or delete any material.

4. **Studying Lectures**
   - View uploaded materials in the list panel.
   - Choose any material from the list and use the following buttons:
     - "Generate Conceptual Example" (GPT-4o powered)
     - "Generate Summary" (GPT-4o powered short/detailed summaries)
     - "Find Contents" (GPT-4o powered content analysis)
   - All generation uses GPT-4o for high-quality, consistent responses
   - After generating the response, check the relevance of the content using the "Check Relevance" button (this button appears after generating a response).
   - Write prompts in the text field below for further analysis on the material.

5. **Quiz**
   - Choose any material from the dropdown list.
   - Select a difficulty level and press "Generate Quiz" to take the quiz.
   - Quiz generation now powered by GPT-4o for improved question quality and accuracy
   - After answering the quiz questions, your score will be displayed.

6. **Assignment**
   - Choose any material from the dropdown list.
   - Press "Generate Conceptual Assignment" to generate an assignment with instructions (GPT-4o powered).
   - The generated assignment will also be available as a PDF.
   - Download the PDF by pressing "Download Generated Assignment (PDF)".
   - Upload your completed assignment below with your name.

7. **Feedback**
   - Submit your feedback anonymously as a student.

### Step-3: Login Again as a Teacher

1. **Quiz**
   - View the quiz responses submitted when logged in as a student.

2. **Assignment**
   - View the assignments submitted when logged in as a student.

3. **Feedback**
   - View the feedback submitted when logged in as a student.

## Technical Architecture

### Backend Components
- **Content Generation**: GPT-4o for all text generation tasks
- **Quiz Generation**: GPT-4o with structured JSON output
- **Quality Evaluation**: LLM-as-Judge (GPT-4o) + Automated Metrics
- **Database**: SQLite for user management and content storage
- **File Storage**: Local file system for PDF materials

### Testing Framework
- **Benchmark Dataset**: 90 comprehensive test cases
- **Task Types**: Summarization, Q&A, Quiz Generation
- **Evaluation Metrics**: LLM scoring (0-10), Word-F1, latency analysis
- **Quality Assessment**: Automated evaluation of generated content

## Running Tests

To run the comprehensive testing framework:

```bash
# Full test suite (90 tests, ~15-30 minutes)
python run_tests.py

# Limited testing (e.g., 5 tests for validation)
python run_tests.py --limit 5

# Generate statistics from existing results
python quick_stats.py
```
