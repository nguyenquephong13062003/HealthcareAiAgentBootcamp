# Healthcare AI Agent - Mini Bootcamp

This repository contains my lab project developed under the guidance of **Satyam Mishra** during a **mini bootcamp** conducted over two sessions offered by Quanskill. The project demonstrates how to build an AI agent in the healthcare domain.

---

## 📅 Bootcamp Information

- **Session 1:** 15 / 03 / 2026  
- **Session 2:** 22 / 03 / 2026  


---

## ⚙️ Tech Stack

- Python  
- Gradio  
- Transformers (FLAN-T5)  
- JSON storage  

---

## 🧩 Project Structure

```text
healthcare_agent/
│── core/
│   ├── diagnostics.py
│   ├── doctors.py
│   ├── insurance.py
│   ├── memory.py
│   ├── explainer.py
│   └── config.py
│── data/
│   ├── doctors.csv
│   ├── insurance.csv
│   ├── medical_knowledge.csv
│── models/
│   ├── insurance_model.pkl
│   ├── symptom_embeddings.npy
│   ├── symptom_index.faiss
│── scripts/
│   └── build_knowledge_index.py
│   └── train_insurance_model.py
│── storage/
│── ui/
│   └── app.py
│── requirements.txt
```

---

# Setup Environment And Run Test

## Session 1

1. Create a virtual environment and instal requirements:
    ```bash
    python -m venv .venv
    .\.venv\Scripts\Activate
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

2. Build the knowledge index:
    ```bash
    python -m scripts.build_knowledge_index
    ```

3. Quick diagnosis test:
    ```bash
    python -c "from core.diagnostics import SymptomDiagnosticEngine; engine=SymptomDiagnosticEngine(); print(engine.diagnose('chest pain and sweating'))"
    ```

4. Quick doctor test:
    ```bash
    python -c "from core.doctors import find_doctors; print(find_doctors('Cardiology','Seoul'))"
    ```

5. Verify file exists:
    ```bash
    Get-Content data\insurance.csv | Select-Object -First 5
    ```

6. Train the model:
    ```bash
    python -m scripts.train_insurance_model
    ```

7. Test the insurance module:
    ```bash
    python -c "from core.insurance import InsuranceEstimator; est=InsuranceEstimator(); print(est.estimate('demo123', 35, 'male', 29.5, 1, 'no', 'southeast'))"
    ```

## Session 2

1. Quick sanity check before Session 2:
    ```bash
    python -c "from core.diagnostics import SymptomDiagnosticEngine; engine=SymptomDiagnosticEngine(); print(engine.diagnose('chest pain and sweating')['top_diagnosis']['specialty'])"
    ```

2. Then run in terminal:
    ```bash
    python -c "from core.insurance import InsuranceEstimator; est=InsuranceEstimator(); print(est.estimate('demo123', 35, 'male', 29.5, 1, 'no', 'southeast')[1])"
    ```

3. Test Deterministic Explanation:
    ```bash
    python -c "from core.explainer import AIExplainer; ex=AIExplainer(); payload={'top_diagnosis': {'diagnosis':'Possible angina or heart-related issue','specialty':'Cardiology','triage_level':'emergency','recommended_tests':'ECG, troponin blood test, chest X-ray','advice':'Seek emergency care immediately.'}, 'doctors':[{'name':'Dr. Park Jihoon','specialty':'Cardiology','city':'Seoul','rating':4.7}], 'insurance_text':'Estimated insurance cost: 5,407', 'history_summary':'No previous visit found.'}; print(ex.explain(payload, use_ai=False))"
    ```

4. Test FLAN-Large raw rewrite:
    ```bash
    python -c "from core.explainer import AIExplainer; ex=AIExplainer(use_local_model=True); payload={'top_diagnosis': {'diagnosis':'Possible angina or heart-related issue','specialty':'Cardiology','triage_level':'emergency','recommended_tests':'ECG, troponin blood test, chest X-ray','advice':'Seek emergency care immediately.'}, 'doctors':[{'name':'Dr. Park Jihoon','specialty':'Cardiology','city':'Seoul','rating':4.7}], 'insurance_text':'Estimated insurance cost: 5,407', 'history_summary':'No previous visit found.'}; print(ex.explain_model_only(payload))"
    ```

5. Test final smart behavior:
    ```bash
    python -c "from core.explainer import AIExplainer; ex=AIExplainer(use_local_model=True); payload={'top_diagnosis': {'diagnosis':'Possible angina or heart-related issue','specialty':'Cardiology','triage_level':'emergency','recommended_tests':'ECG, troponin blood test, chest X-ray','advice':'Seek emergency care immediately.'}, 'doctors':[{'name':'Dr. Park Jihoon','specialty':'Cardiology','city':'Seoul','rating':4.7}], 'insurance_text':'Estimated insurance cost: 5,407', 'history_summary':'No previous visit found.'}; print(ex.explain(payload, use_ai=True))"
    ```

# Run the app

- In terminal, from the project root:
    ```bash
    python -m ui.app
    ```

- Expected output should show something like:
    ```bash
    Running on local URL: http://127.0.0.1:7860
    ```

- Open [http://127.0.0.1:7860](http://127.0.0.1:7860) in your browser.

## 👤 Author

Name: **Nguyễn Quế Phong**
- Email: [nguyenquephong13062003@gmail.com](mailto:nguyenquephong13062003@gmail.com)
- Github: [nguyenquephong13062003](https://github.com/nguyenquephong13062003)

---


## 🙏 Acknowledgements

I would like to express my sincere gratitude to three outstanding mentors who made this mini bootcamp an incredibly valuable experience.

- **Mr. Satyam Mishra** - PhD Researcher at KAIST (South Korea)
- **Mr. Châu Văn Vân** – PhD Candidate in Information & Data Science @ KMUTNB (Thailand)
- **Mr. Nguyễn Hoàng Giang** – Lecturer in Business Administration at FPT University

---