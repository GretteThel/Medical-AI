# Medical-AI - Live Code Experiment

This project demonstrates how to use **Google’s Gemini 2.5 Flash** multimodal model for **AI-assisted medical image interpretation**.  
It explores how generative AI can assist radiologists in analyzing X-rays and other clinical images using both visual and structured patient data.

---

## Features
- Uses **Gemini 2.5 Flash** via the `google-generativeai` library
- Accepts **both text and image inputs** for multimodal reasoning
- Performs **radiological analysis**, identifying:
  - Type of imaging (e.g., X-ray, MRI)
  - Visible anatomical structures
  - Abnormalities and findings
  - Recommended next steps
- Integrates **patient metadata** (`metadata.csv`) for contextual interpretation

---

## Project Workflow
1. **Install dependencies**
   ```python
   !pip install -q google-generativeai pillow pandas requests
    ````
2. **Initialize Gemini model**

   ```python
   import google.generativeai as genai
   genai.configure(api_key="YOUR_API_KEY")
   model = genai.GenerativeModel("gemini-2.5-flash")
   ```
3. **Load a medical image**

   ```python
   from PIL import Image
   import requests
   image_url = "https://upload.wikimedia.org/wikipedia/commons/c/c8/Chest_Xray_PA_3-8-2010.png"
   image = Image.open(requests.get(image_url, stream=True).raw)
   ```
4. **Generate a radiology report**

   ```python
   prompt = "You are an expert radiologist. Describe this X-ray..."
   response = model.generate_content([prompt, image])
   print(response.text)
   ```
5. **Combine with patient data**

   ```python
   import pandas as pd, json
   patient_data = pd.read_csv("metadata.csv")
   pat_11 = patient_data.loc[11].to_dict()
   prompt3 = f"You are an expert radiologist. PATIENT DATA: {json.dumps(pat_11, indent=2)}"
   response = model.generate_content([prompt3, image])
   ```
---

## Applications

* Medical education & workshops
* Prototype radiology assistants
* Context-aware image-text analysis
* Explainable AI in healthcare

---

## Disclaimer

This notebook is for **educational and research purposes only**.
It **does not provide medical advice** or diagnostic recommendations.
Use responsibly and in compliance with applicable regulations.

---

## Author

**Grethel Mabilangan**
AI & Data Science Enthusiast


```
