# GPT Client BuildPlan v3.1

## 🎯 Doel van het Project

Bouw een hybride Windows-desktopapplicatie die fungeert als operator-gestuurde frontend voor de OpenAI API.  
De app moet:
- ✅ AI-output genereren op basis van vrije tekstprompts en text/json file upload via filepicker
- ✅ Input can contain sourcecode, multilines, powershell and prompts
- ✅ Bestanduitvoer automatisch verwerken (inclusief bestandsnaam uit response)
- ✅ Python openai-sdk gebruiken waar nodig
- ✅ Volledig lokaal functioneren met veilige bestands-I/O
- ✅ Foutafhandeling, logging en testbaarheid volgens ISO/IEEE normen ondersteunen

---

## 📁 Projectstructuur (bestanden en componenten)

| Bestand              | Doel |
|----------------------|------|
| `main.ps1`           | Windows Forms GUI (PowerShell), hoofdinterface met operator |
| `bridge.py`          | Python bridge naar OpenAI API, met JSON I/O, based on openai-sdk |
| `settings.json`      | Configuratiebestand: API-sleutel, outputpad, model |
| `README.md`          | Deze build- en gebruiksinstructie |
| `LICENSE.txt`        | Licentieinformatie |
| `testresults/`       | Output van testcases |
| `.testspec.json`     | (optioneel) Testscenario's per component en build |

---

## 🖥️ GUI Specificaties (`main.ps1`)

- 🧾 **InputBox**: multiline prompt invoer
- 📤 **OutputBox**: toont response (kleurgecodeerd)
- 🧠 **HistoryBox**: toont voorgaande prompts + antwoorden
- 💾 **SaveButton**: schrijft response naar bestand (bestandsnaam uit JSON-response)
- 🧰 **ModelDropdown**: keuze uit beschikbare modellen
- ⚙️ **ConfigTab**: voor API key, pad en instellingen
-  **Fileselection**: voor import txt/json
-  **Directoryselection**: voor other output folder then default d:\dev\output\

> apikey location: `d:\dev\its\its.txt`  
> Formaat daarin: enkel `{"key": "<APIKEY>"}` (JSON)

---

## 🧠 OpenAI Integratie

### Parameters:
- `temperature`: **0.0** (deterministisch)
- `max_tokens`: maximum toegestaan
- `model`: `"gpt-4"`, `"gpt-4o"` etc. (instelbaar via dropdown)
- Response wordt geïnterpreteerd als:
  ```json
  {
    "filename": "example.py",
    "content": "<bestandinhoud>"
  }
