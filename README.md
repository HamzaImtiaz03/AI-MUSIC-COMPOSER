# AI Music Composer: Generative AI for Custom Melodies

![AI Music Composer Banner](https://github.com/HamzaImtiaz03/AI-MUSIC-COMPOSER/blob/main/Project%20Tech%20Stacks%20Image.png?raw=true) <!-- Replace with actual image URL or embed if available -->

[![GitLab Repo](https://img.shields.io/badge/GitLab-Repo-orange?logo=gitlab)](https://gitlab.com/HamzaImtiaz03/AI-Music-Composer) <!-- Update with actual repo URL -->
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11](https://img.shields.io/badge/Python-3.11-green?logo=python)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue?logo=docker)](https://www.docker.com/)
[![Kubernetes Deployed](https://img.shields.io/badge/Deployed-Kubernetes-orange?logo=kubernetes)](https://kubernetes.io/)
[![GCP Hosted](https://img.shields.io/badge/Hosted-GCP-brightgreen?logo=google-cloud)](https://cloud.google.com/)
[![GitLab CI/CD](https://img.shields.io/badge/CI%2FCD-GitLab-orange?logo=gitlab)](https://gitlab.com/)

## Overview

The **AI Music Composer** is a groundbreaking generative AI system that creates personalized music compositions based on user descriptions and selected styles. Harnessing the power of large language models (LLMs) via LangChain and Groq, it generates melodies, harmonies, rhythms, and adapts them to styles like Sad, Happy, Jazz, Romantic, or Extreme. The output is synthesized into playable WAV audio, providing an immersive creative experience.

This project exemplifies end-to-end MLOps, integrating AI development with automated deployment pipelines. From a Streamlit-based interactive UI to containerized deployment on Google Kubernetes Engine (GKE) using Docker, GitLab CI/CD for continuous integration/delivery, and secure configurations, it ensures scalability and reliability. Perfect for musicians, composers, educators, or AI enthusiasts exploring generative music in entertainment and media.

## Key Features

- **AI-Driven Composition**: Uses LangChain and Groq to generate melodies, harmonies, and rhythms from natural language inputs, with style adaptation for diverse outputs.
- **Audio Synthesis**: Converts generated notes to frequencies and synthesizes WAV audio using libraries like music21 and synthesizer.
- **Interactive Frontend**: Streamlit app for user inputs, real-time generation, audio playback, and composition summaries.
- **Utility Functions**: Includes note-to-frequency conversion, WAV generation, and custom logging/exceptions for robustness.
- **Secure Configurations**: Environment variables and Kubernetes secrets for API keys (e.g., GROQ_API_KEY).
- **Automated CI/CD**: GitLab pipeline for code checkout, Docker image build/push to Artifact Registry, and deployment to GKE.
- **Containerization & Orchestration**: Dockerized app with Kubernetes Deployment (1 replica) and LoadBalancer Service for high availability.
- **Cloud-Native Deployment**: Hosted on GKE with pre-configured GCP services, clusters, and registries.

## Architecture

The project is structured across setup, utilities, logic, application, containerization, and CI/CD phases, as illustrated below:

![Project Architecture Flowchart](https://github.com/HamzaImtiaz03/AI-MUSIC-COMPOSER/blob/main/111%20-%20Introduction%20to%20the%20Project%20-%20AI+Music+Composer+Workflow.png?raw=true) <!-- Replace with actual image URL or embed -->

### High-Level Breakdown:
1. **Setup Steps**: Project/API initialization, virtual environment, logging, custom exceptions, library installation, Groq API integration.
2. **Utility Functions**: Note-to-frequency conversion, WAV audio generation, music21 library usage, synthesizer integration.
3. **Music Logic**: MusicLLM class for melody/harmony/rhythm generation and style adaptation using LangChain/Groq.
4. **Application Layer**: Streamlit app for UI and main logic.
5. **Containerization**: Dockerfile for image building.
6. **CI/CD Pipeline**: GitLab CI/CD for checkout, build, push to GAR, and GKE deployment.
7. **Orchestration**: Kubernetes manifests for deployment and service.

This architecture promotes modularity, automation, and seamless scaling.

## Technologies Used

- **AI/ML Frameworks**: LangChain (core, community, Groq integration), music21 (music notation), synthesizer (audio generation), SciPy (signal processing).
- **Frontend**: Streamlit (interactive web apps).
- **Environment Management**: Python-dotenv (secrets handling).
- **Containerization & Orchestration**: Docker (containerization), Kubernetes (GKE deployments), Kubectl (management).
- **CI/CD**: GitLab CI/CD (pipelines with GCP integration).
- **Cloud Platform**: Google Cloud Platform (GKE, Artifact Registry, Compute Engine, etc.).
- **Version Control**: GitLab.
- **Packaging**: Setuptools (via setup.py).

Full dependencies are listed in `requirements.txt`.

## Installation

### Prerequisites
- Python 3.11+
- Git
- Docker (for containerization)
- Google Cloud Platform Account (for deployment)
- API Keys: Groq (stored in `.env`)
- Optional: Kubectl, gcloud CLI for local GKE testing

### Steps
1. **Clone the Repository**:
   ```
   git clone https://gitlab.com/HamzaImtiaz03/AI-Music-Composer.git <!-- Update with actual repo URL -->
   cd AI-Music-Composer
   ```

2. **Set Up Virtual Environment** (Recommended):
   ```
   python -m venv venv
   source venv/bin/activate  # On Unix/Mac
   # Or on Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:
   ```
   pip install -e .
   ```

4. **Configure Environment Variables**:
   Create a `.env` file in the root directory:
   ```
   GROQ_API_KEY=your_groq_api_key
   # Add other variables as needed
   ```

## Usage

1. **Run the Application Locally**:
   ```
   streamlit run app.py
   ```
   - Access the app at `http://localhost:8501`.
   - Describe the music (e.g., "A soothing piano piece"), select a style, and generate.

2. **Example Interactions**:
   - Input: "Epic orchestral theme", Style: Extreme → Generates melody, harmony, rhythm, and WAV audio.
   - View composition summary and play the audio directly in the app.

3. **Customization**:
   - Modify generation logic in MusicLLM class.
   - Extend styles or integrate additional audio libraries.

## Deployment

This project features an automated CI/CD pipeline for deployment to GKE via GitLab.

### Prerequisites
- GCP Project with enabled APIs (Kubernetes Engine, Container Registry, etc.) as per `FULL_DOCUMENTATION.md`.
- GKE Cluster and Artifact Registry created.
- Service Account with roles (Storage Admin, Artifact Registry Admin, etc.) and JSON key (Base64-encoded for CI/CD).
- GitLab account with project setup.

### Pipeline Overview (via .gitlab-ci.yml)
1. **Checkout Code**: Pull from GitLab.
2. **Build Docker Image**: Authenticate GCP, build, and push to Artifact Registry.
3. **Deploy to GKE**: Configure cluster access, apply Kubernetes YAML.

### Detailed Steps
- Follow `FULL_DOCUMENTATION.md` for GitLab setup, GCP configurations, service account creation, Base64 key encoding, CI/CD variables (GCP_SA_KEY), and Kubernetes secrets.
- Build and run Docker image locally:
  ```
  docker build -t ai-music-composer .
  docker run -p 8501:8501 ai-music-composer
  ```
- Deploy to GKE:
  ```
  gcloud container clusters get-credentials your-cluster --region your-region --project your-project
  kubectl create secret generic llmops-secrets --from-literal=GROQ_API_KEY=your_key
  kubectl apply -f kubernetes-deployment.yaml
  ```
- Trigger pipeline via GitLab push or manual run; monitors workloads in GKE.
- Access the app via the LoadBalancer external IP on port 80.

## Contributing

Contributions are encouraged to refine music generation, add features, or enhance pipelines! To contribute:
1. Fork the repository on GitLab.
2. Create a feature branch (`git checkout -b feature/YourFeature`).
3. Commit changes (`git commit -m 'Add YourFeature'`).
4. Push to the branch (`git push origin feature/YourFeature`).
5. Open a Merge Request.

Adhere to code standards and include tests/documentation.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Frameworks: LangChain, Groq, music21, synthesizer, Streamlit, SciPy.
- Tools: Docker, Kubernetes, GitLab CI/CD, GCP (GKE, Artifact Registry).
- Inspired by generative AI in music composition for creative and educational applications.

For inquiries or support, open an issue on GitLab or contact [Hamza Imtiaz](mailto:hamzaimtiaz8668@gmail.com).

---

*Built by Hamza Imtiaz | Composing the Future of Music with AI*