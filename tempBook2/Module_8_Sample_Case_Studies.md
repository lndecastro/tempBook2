# Module 8 — Sample Case Studies and Applications of AI

Artificial Intelligence is transforming every sector of society — from education and healthcare to environmental management, business, and the arts.
This module provides **hands-on, ready-to-run case studies** where you can explore data, run code, and design prompts to experience AI-assisted analysis and creation in action.

> All datasets are **synthetic/anonymized** and for **educational use** only.

[⬇️ Download all case-study data (ZIP)](ai_literacy_case_studies.zip)

---

## 🎯 Learning Objectives

:::{admonition} After completing this module, you will be able to:
- Apply AI tools and prompt engineering techniques to real-world case studies.
- Run data analyses using the provided datasets for education, healthcare, environment, business, and arts.
- Evaluate how prompt design and context affect AI performance.
- Reflect on ethical, social, and environmental implications of AI applications.
:::

---

## 🧑‍🏫 Case Study 1 — Education: Course Companion & Lesson Plan Review

**Files (in the ZIP):**
- education/syllabus.txt
- education/rubric.txt
- education/lesson_plan.md

### A) Prompt
```
System role: You are an instructional designer for higher education.

Context files you can reference:
- Syllabus (excerpt): [paste the text from syllabus.txt]
- Writing Rubric (excerpt): [paste the text from rubric.txt]

Task:
1) Review the lesson_plan.md (pasted below) against the syllabus goals and the rubric criteria.
2) Summarize the lesson plan in 3 bullet points for students.
3) Produce a table with columns: Strengths | Weaknesses | Improvement Suggestions.
4) Write a 60-word student-facing overview.

Lesson Plan:
[Paste the contents of lesson_plan.md]
```

### B) Mini Analysis (Python)
```python
import pandas as pd, pathlib
base = pathlib.Path("ai_literacy_case_studies/education")
print(open(base/"syllabus.txt").read())
print(open(base/"rubric.txt").read())
print(open(base/"lesson_plan.md").read())
```

---

## 🩺 Case Study 2 — Healthcare: Clinical Summary (Educational Only)

**Files:**
- healthcare/patient_records.csv
- healthcare/guideline.txt

> ⚠️ Educational disclaimer: synthetic data; **not** medical advice; always require **human expert review**.

### A) Prompt
```
System role: You are a clinical data analyst supporting a hospital quality-improvement team.
Ethical boundary: Educational exercise only; do not provide medical advice.

Reference: Clinical Guideline (simplified): 
[Paste the text from guideline.txt]

Task:
1) Read the CSV rows pasted below (anonymized patient_records.csv).
2) For each case, summarize under: Key Findings | Potential Risks | Next Steps (guideline-aligned).
3) Flag any “red flags” that require escalation per the guideline.
4) End with a 2-sentence caveat emphasizing human review.
```

### B) Mini Analysis (Python)
```python
import pandas as pd, pathlib
base = pathlib.Path("ai_literacy_case_studies/healthcare")
df = pd.read_csv(base/"patient_records.csv")
print(df.head(3).to_string(index=False))
```

---

## 🌿 Case Study 3 — Environment: Water Quality Early Warning

**Files:**
- environment/water_quality.csv

### A) Prompt
```
System role: You are an environmental data analyst.
Goal: Detect anomalies suggestive of potential algal bloom risk.

Task:
1) I will paste a dataframe sample from water_quality.csv (site, date, chlorophyll_a, temp_c, nitrate_mgL, phosphate_mgL).
2) Propose a simple anomaly detection approach using z-scores for chlorophyll_a within each site.
3) Suggest domain-informed thresholds to flag potential risk for review.
4) Draft a concise report: Summary | Sites of Interest | Recommended Next Checks.
```

### B) Mini Analysis (Python)
```python
import pandas as pd, numpy as np, pathlib
base = pathlib.Path("ai_literacy_case_studies/environment")
df = pd.read_csv(base/"water_quality.csv")
df['date'] = pd.to_datetime(df['date'])
df['chl_site_mean'] = df.groupby('site')['chlorophyll_a'].transform('mean')
df['chl_site_std'] = df.groupby('site')['chlorophyll_a'].transform('std').replace(0, 1e-6)
df['chl_z'] = (df['chlorophyll_a'] - df['chl_site_mean'])/df['chl_site_std']
df['chl_flag'] = (df['chl_z'].abs() >= 2.0)
summary = df.groupby('site')['chl_flag'].sum().rename('anomaly_count')
print(summary)
print(df.loc[df['chl_flag'], ['date','site','chlorophyll_a','chl_z']])
```

---

## 💼 Case Study 4 — Business: Customer Feedback Insights

**Files:**
- business/customer_feedback.csv

### A) Prompt
```
System role: You are a customer insights analyst.

Task:
1) I will paste a sample of customer_feedback.csv (product, feedback).
2) Cluster feedback into 3–5 themes with short labels.
3) Produce a table: Theme | Representative Quote | Suggested Action.
4) Write a 100-word executive summary.
```

### B) Mini Analysis (Python)
```python
import pandas as pd, pathlib
base = pathlib.Path("ai_literacy_case_studies/business")
df = pd.read_csv(base/"customer_feedback.csv")
print(df.head().to_string(index=False))
print(df['product'].value_counts())
```

---

## 🎨 Case Study 5 — Arts: Story Seeds to Short Scene

**Files:**
- arts/story_seeds.csv

### A) Prompt
```
System role: You are a creative writing coach.

Task:
1) Here are story seeds (character, trait, goal) from a CSV.
2) Pick one seed and outline a scene (setting, conflict, turning point, resolution beat) in ~120 words.
3) Keep tone grounded and sensory-rich.
4) End with two “next-scene” options.
```

### B) Mini Analysis (Python)
```python
import pandas as pd, pathlib
base = pathlib.Path("ai_literacy_case_studies/arts")
seeds = pd.read_csv(base/"story_seeds.csv")
print(seeds.to_string(index=False))
```

---

## ✅ Submission & Reflection

- Include your **prompt(s)**, **AI outputs**, and **Python outputs**.
- Reflect (150–200 words): How did prompt and context choices shape your results?
- Note limitations, assumptions, or ethical considerations.

---

## 📘 Further Reading

- World Economic Forum (2024). *AI Governance and the Future of Work.*
- UNESCO (2023). *Guidelines for AI in Education and Research.*
- Nature Editorial (2023). *Artificial Intelligence in Science: Opportunities and Pitfalls.*
- Mollick, E. & Mollick, L. R. (2024). *Co-Intelligence: Living and Working with AI.*
- European Commission (2024). *Ethics Guidelines for Trustworthy AI.*
- Dendritic Institute (2025). *AI Literacy Series – Module 8: Hands-on Case Studies.*

## Reflection

> Which of these case studies feels most relevant to your field or future career?  
> How might you apply similar principles in your own work or research?  
> What challenges or safeguards would you need to ensure responsible AI use?

Reflect on how the lessons from these cases — transparency, context, and collaboration — can guide your personal or organizational approach to AI adoption.

---

## 📘 Further Reading

- World Economic Forum (2024). *Shaping the future of artificial intelligence: Reflections from the AI Governance Alliance.*, https://www.weforum.org/stories/2024/06/ai-governance-alliance-future-of-ai/  
- UNESCO (2023). *Guidelines for AI in Education and Research.*, https://www.unesco.org/en/articles/guidance-generative-ai-education-and-research  
- European University Association (2023). *Artificial Intelligence in Science. Challenges, Opportunities and the Future of Research.*, https://www.eua.eu/news/member-and-partner-news/artificial-intelligence-in-science-challenges-opportunities-and-the-future-of-research.html  
- Mollick, E. & Mollick, L. R. (2024). *Co-Intelligence: Living and Working with AI.*, Portfolio. 
- European Commission (2019). *Ethics Guidelines for Trustworthy AI.*, https://digital-strategy.ec.europa.eu/en/library/ethics-guidelines-trustworthy-ai  
- Dendritic Institute (2025). *AI Literacy Series – Module 8: Sample Case Studies and Applications of AI.* (Slides & video lecture)
