# AI-Powered Resume & Cover Letter Agent

A sophisticated automation workflow that leverages Large Language Models (LLMs) to instantly tailor a master resume and cover letter to a specific job description, significantly increasing application efficiency and effectiveness.

---

## 🎯 The Problem

In today's competitive job market, submitting a generic resume is a recipe for rejection. Recruiters and Applicant Tracking Systems (ATS) prioritize applications that are highly tailored to the specific language and requirements of a job description.

However, manually customizing a resume and cover letter for every single application is an incredibly tedious and time-consuming process. This often leads to burnout and a lower quality of applications.

## 💡 The Solution

This project solves the problem by creating an intelligent agent within **n8n.io** that automates the entire tailoring process. The agent acts as a personal HR assistant, performing the following steps in seconds:

1.  **Intake:** Accepts a master LaTeX resume and a target job description as inputs.
2.  **Analysis:** Uses the **Google Gemini Pro** API to perform a deep analysis of the job description, extracting key skills, technologies, and responsibilities.
3.  **Resume Generation:** Intelligently modifies the master LaTeX resume, re-phrasing bullet points and re-ordering sections to align perfectly with the extracted keywords and themes.
4.  **Cover Letter Drafting:** Generates a compelling, three-paragraph cover letter that is specifically targeted to the role and company, referencing the most critical requirements from the job description.
5.  **File Conversion & Delivery:** Automatically converts the generated `.tex` files into professional `.pdf` documents using **CloudConvert** and prepares them for delivery.

This workflow transforms a multi-hour task into a one-click process, enabling rapid, high-quality job applications at scale.

## 🛠️ Tech Stack

* **Automation & Orchestration:** [n8n.io](https://n8n.io/)
* **AI Language Model:** [Google Gemini Pro](https://deepmind.google/technologies/gemini/)
* **File Conversion:** [CloudConvert API](https://cloudconvert.com/)
* **Document Format:** LaTeX

## ⚙️ Setup & Configuration

To get this project running, you will need to import the workflow into your own n8n instance and configure the necessary API keys.

**1. Clone the Repository:**

```bash
git clone [https://github.com/your-username/ai-resume-agent.git](https://github.com/your-username/ai-resume-agent.git)
cd ai-resume-agent
```

**2. Import the Workflow:**

* In your n8n dashboard, go to **Workflows** and click **Import from File**.
* Select the `workflow.json` file from this repository.

**3. Configure API Keys (CRITICAL):**
This workflow requires API access to several services.

* **Google Gemini:** The Google Gemini node is configured to use the n8n credential manager, which is the most secure method.
    * Navigate to the **Credentials** section in your n8n settings.
    * Click **Add credential** and create a "Google Gemini API" credential using your API key.
    * In the workflow, select your newly created credential from the dropdown menu in the Gemini node.

* **CloudConvert:** The workflow uses an HTTP Request node to interact with the CloudConvert API via a Bearer Token. To avoid exposing your key in the `workflow.json` file, you must load it dynamically.
    * Go to the HTTP Request node responsible for CloudConvert.
    * Under "Authentication", select "Header Auth".
    * For the "Name" field, enter `Authorization`.
    * For the "Value" field, use an n8n expression to load your key from a secure source, like an environment variable: `Bearer {{$env.CLOUDCONVERT_API_KEY}}`.

## 🚀 Usage

1.  Open the "AI Resume Agent" workflow in n8n.
2.  Click **"Test workflow"** or **"Execute workflow"**.
3.  The workflow will prompt you for the required inputs:
    * Your master resume content (LaTeX).
    * The full job description text.
4.  Once the workflow completes, the generated PDF files will be available in the output of the final nodes.

## 🔮 Future Work

* **Frontend UI:** Build a simple web interface (using React or Vue.js) that allows a user to interact with the agent without needing to open n8n.
* **Vector Database Integration:** Store multiple versions of resumes and job descriptions in a vector database (e.g., Pinecone) to provide more context and improve the quality of generated content over time.
* **Direct Application Submission:** Integrate with Greenhouse or Lever APIs to automate the final step of submitting the application.
