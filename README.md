# Tweet Generator with Strict JSON Validation

This project provides a robust, LLM-driven tweet generator that enforces strict JSON schema validation using Pydantic. It ensures every generated tweet response is a valid, well-formed JSON object matching an exact schema, with strong error handling and retry logic.

## Features

- **Strict JSON Output:** LLM is prompted to return only JSON with exact keys: `tweet`, `word_count`, `sentiment`.
- **Pydantic Validation:** All responses are validated using Pydantic models for type, length, and value constraints.
- **Error Handling:** Handles malformed JSON, schema violations, and custom validation (e.g., word count accuracy).
- **Retry Logic:** Automatically retries up to 2 times on validation failure.
- **Prompt Engineering:** Enhanced prompts and system messages to maximize LLM compliance.
- **Test Suite:** Includes edge case and error handling tests.

---

## JSON Schema

```json
{
  "tweet": "string (1-280 chars, required)",
  "word_count": "integer (>0, required, must match actual tweet word count)",
  "sentiment": "string (one of: 'positive', 'negative', 'neutral', required)"
}
```

### Example

```json
{
  "tweet": "Excited to share our new product launch today!",
  "word_count": 8,
  "sentiment": "positive"
}
```

---

## Usage

1. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

2. **Run the demo**
   ```bash
   python main.py
   ```
   - Generates a tweet, validates the JSON, and demonstrates error handling.

3. **Run tests**
   ```bash
   pytest tests/test_validation.py
   ```

---

## File Overview

- `models.py` — Pydantic models for response validation.
- `tweet_generator.py` — LLM prompt engineering, JSON parsing, validation, and retry logic.
- `main.py` — Demo script with validation and error handling examples.
- `tests/test_validation.py` — Unit tests for edge cases and error handling.
- `requirements.txt` — Python dependencies.

---

## Error Handling

- **Malformed JSON:** Catches and reports JSON parsing errors.
- **Schema Violations:** Raises `ValidationError` for missing/invalid fields.
- **Custom Validation:** Ensures `word_count` matches actual tweet word count.
- **Retries:** On failure, retries up to 2 times before raising an error.

---

## License

This project is licensed under the terms of the MIT License. See the [LICENSE](LICENSE) file for details.

