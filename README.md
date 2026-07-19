# Awesome PII Tools [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of tools and resources for working with personally identifiable information: PII detection, data anonymization, masking, pseudonymization, and synthetic data — so you can use production-like data without leaking production data.

Anonymizing data is a daily need for developers and data engineers: refreshing test environments from production, sharing datasets, feeding logs into analytics, or stripping PII before sending text to an LLM. Regulations like **GDPR**, **CCPA**, and **HIPAA** make it mandatory — but the tooling is scattered. This list brings it together.

## Contents

- [PII Detection & Redaction](#pii-detection--redaction)
- [Database Anonymization](#database-anonymization)
- [Fake Data Generation](#fake-data-generation)
- [Synthetic Data](#synthetic-data)
- [LLM & AI Pipelines](#llm--ai-pipelines)
- [Differential Privacy](#differential-privacy)
- [Document, Image & Media Redaction](#document-image--media-redaction)
- [Research & Statistical Anonymization](#research--statistical-anonymization)
- [Commercial Platforms](#commercial-platforms)
- [Learning Resources](#learning-resources)
- [Related Awesome Lists](#related-awesome-lists)

## PII Detection & Redaction

Detect and remove personally identifiable information from unstructured text.

- [Microsoft Presidio](https://github.com/microsoft/presidio) - Open-source framework for PII detection and anonymization in text, images, and structured data. 50+ built-in recognizers (names, credit cards, SSNs, phone numbers), pluggable NER backends (spaCy, transformers), and a separate anonymizer module for masking, hashing, or encrypting findings.
- [Philter](https://github.com/philterd/philter) - Self-hosted PII/PHI redaction engine with an API. Packaged and deployable, aimed at teams that want redaction without building a pipeline from library parts.
- [scrubadub](https://github.com/LeapBeyond/scrubadub) - Python library for removing PII from free text using pluggable detectors.
- [DataFog](https://github.com/DataFog/datafog-python) - Open-source PII detection and anonymization for text pipelines.
- [GLiNER](https://github.com/urchade/GLiNER) - Zero-shot named entity recognition model widely used for PII detection; PII-specific fine-tunes cover 55+ entity types and can serve as a Presidio backend.
- [StarPII](https://huggingface.co/bigcode/starpii) - NER model trained to detect PII in source code — names, emails, keys, and secrets in repositories.

## Database Anonymization

Anonymize entire databases or dumps — the classic "prod data in the test environment" problem.

- [PostgreSQL Anonymizer](https://gitlab.com/dalibo/postgresql_anonymizer) - Postgres extension implementing "privacy by design": masking rules declared inside the schema via `SECURITY LABEL`. Supports dynamic masking, static masking, anonymous dumps, masking views, and replica masking. Rewritten in Rust as of 2.0.
- [Greenmask](https://github.com/GreenmaskIO/greenmask) - Go-based utility for logical dump anonymization with deterministic transformations and validation. Zero database changes required; integrates cleanly into CI/CD; backward-compatible with standard Postgres utilities.
- [Neosync](https://github.com/nucleuscloud/neosync) - Open-source platform to anonymize production data and sync it across environments for Postgres and MySQL, with synthetic data generation and referential integrity handling.
- [nxs-data-anonymizer](https://github.com/nixys/nxs-data-anonymizer) - Stream-based anonymizer for PostgreSQL and MySQL/MariaDB dumps. Pipe `pg_dump` through it straight into your dev database; rules use Go templates with the Sprig library. Ships with GitLab CI and GitHub Actions integration examples.
- [pganonymize](https://github.com/rheinwerk-verlag/pganonymize) - Command-line tool for anonymizing PostgreSQL databases using a YAML schema definition.
- [pg-anonymizer](https://github.com/rap2hpoutre/pg-anonymizer) - Node.js CLI that dumps an anonymized PostgreSQL database in one command.
- [Anonimatron](https://github.com/realrolfje/anonimatron) - Java-based, GDPR-oriented database anonymizer producing consistent pseudonyms across runs, so relations between tables stay intact.
- [MySQL/MariaDB dynamic masking via ProxySQL](https://proxysql.com/documentation/data-masking/) - Pattern for masking sensitive columns at the proxy layer without touching the schema.

## Fake Data Generation

Generate realistic fake values to substitute for real ones.

- [Bogus](https://github.com/bchavez/Bogus) - Fluent fake data generator for .NET (C#, F#, VB.NET), ported from faker.js.
- [Datafaker](https://github.com/datafaker-net/datafaker) - Modern fake data library for the JVM (successor to java-faker).
- [Faker (Python)](https://github.com/joke2k/faker) - The canonical fake data library: names, addresses, companies, credit cards, in dozens of locales.
- [Faker.js](https://github.com/faker-js/faker) - Community-maintained fake data generator for JavaScript/TypeScript.
- [kotlin-faker](https://github.com/serpro69/kotlin-faker) - Fake data generation for Kotlin and the JVM.
- [Mimesis](https://github.com/lk-geimfari/mimesis) - High-performance fake data generator for Python with strong locale support and schema-based generation.

## Synthetic Data

Generate entirely artificial datasets that preserve statistical properties of the original.

- [SDV (Synthetic Data Vault)](https://github.com/sdv-dev/SDV) - Python ecosystem for generating synthetic tabular, relational, and time-series data using ML models, with quality/privacy evaluation metrics.
- [Synthea](https://github.com/synthetichealth/synthea) - Synthetic patient generator producing realistic (but fully artificial) medical histories — a standard in healthcare development.
- [ydata-synthetic](https://github.com/ydataai/ydata-synthetic) - Synthetic tabular and time-series data generation using GANs.
- [nbsynthetic](https://github.com/NextBrain-ai/nbsynthetic) - Simple synthetic tabular data generation aimed at small datasets.

## LLM & AI Pipelines

Strip sensitive data from prompts, training data, and model outputs.

- [LLM Guard](https://github.com/protectai/llm-guard) - Toolkit of 35+ input/output scanners for LLM applications, including PII anonymization, secrets detection, and toxicity checks.
- [Ollama](https://github.com/ollama/ollama) - Run LLMs entirely on your own hardware. The foundation for privacy-preserving PII workflows: sensitive text can be classified, redacted, or rewritten by a local model without ever leaving your perimeter — often the only LLM option compliance will approve.
- [LLMAIx / LLM-Anonymizer](https://github.com/KatherLab/LLMAIx) - De-identifies clinical documents using locally hosted LLMs, demonstrating that on-prem models can match or beat rule-based PHI redaction (published in NEJM AI).
- [Awesome Anonymization for LLMs](https://github.com/malteos/awesome-anonymization-for-llms) - Curated resources for PII detection and privacy-preserving techniques specifically in LLM applications — complements this list.
- [Presidio + GLiNER integration](https://microsoft.github.io/presidio/) - Documented pattern combining Presidio's pipeline management with GLiNER's detection accuracy for production LLM redaction.

## Differential Privacy

Add mathematically calibrated noise so aggregate analysis works but individuals can't be re-identified.

- [OpenDP](https://github.com/opendp/opendp) - Library of differential privacy algorithms from the OpenDP Project (Harvard), powering the SmartNoise ecosystem.
- [Google Differential Privacy](https://github.com/google/differential-privacy) - Google's libraries for generating differentially private statistics (C++, Go, Java), plus the Privacy on Beam framework.
- [diffprivlib](https://github.com/IBM/differential-privacy-library) - IBM's general-purpose differential privacy library for Python, including DP versions of scikit-learn models.
- [pg_diffix](https://github.com/diffix/pg_diffix) - PostgreSQL extension implementing dynamic anonymization with differential-privacy-inspired guarantees for direct SQL queries.

## Document, Image & Media Redaction

- [Presidio Image Redactor](https://microsoft.github.io/presidio/image-redactor/) - Redacts PII text inside images and DICOM medical images.
- [PDF Redact Tools](https://github.com/firstlookmedia/pdf-redact-tools) - Convert documents to images and back to safely redact PDFs (archived but instructive on why "black box" redaction fails).
- [ocrmypdf](https://github.com/ocrmypdf/OCRmyPDF) - OCR layer for scanned PDFs — commonly the first step in a document redaction pipeline.

## Research & Statistical Anonymization

Classic anonymization models: k-anonymity, l-diversity, t-closeness.

- [ARX](https://github.com/arx-deidentifier/arx) - Comprehensive open-source tool for anonymizing structured data with k-anonymity, l-diversity, t-closeness, and differential privacy, with a full GUI. A standard in academic and healthcare settings.
- [Amnesia](https://amnesia.openaire.eu/) - Anonymization tool from OpenAIRE supporting k-anonymity and km-anonymity with a visual workflow.
- [sdcMicro](https://github.com/sdcTools/sdcMicro) - R package for statistical disclosure control, used by national statistics offices.

## Commercial Platforms

Not open source, but worth knowing when evaluating options.

- [Tonic.ai](https://www.tonic.ai/) - Test data platform: anonymization/subsetting (Structural), NER-based text redaction (Textual), LLM-generated synthetic data (Fabricate). Broadest database support in the space — Postgres, MySQL, SQL Server, Oracle, MongoDB, Snowflake, BigQuery, and more.
- [Gretel](https://gretel.ai/) - Synthetic data and privacy engineering APIs.
- [MOSTLY AI](https://mostly.ai/) - Synthetic data generation platform with a free tier; also maintains an open-source SDK.
- [Private AI](https://www.private-ai.com/) - De-identification platform redacting 50+ PII entity types, deployable on-prem.
- [Skyflow](https://www.skyflow.com/) - Data privacy vault for storing and tokenizing sensitive data with later retrieval.

## Learning Resources

- [GDPR Article 4 & Recital 26](https://gdpr-info.eu/recitals/no-26/) - The legal distinction between anonymization (out of GDPR scope) and pseudonymization (still personal data) — the single most important concept to get right.
- [EDPB Guidelines on Pseudonymisation](https://www.edpb.europa.eu/) - European Data Protection Board guidance on pseudonymization techniques.
- [NIST De-Identification of Personal Information (IR 8053)](https://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.8053.pdf) - Foundational overview of de-identification terminology and techniques.
- [k-Anonymity: A Model for Protecting Privacy (Sweeney, 2002)](https://dataprivacylab.org/dataprivacy/projects/kanonymity/kanonymity.pdf) - The paper that started formal anonymization models.
- [The Netflix Prize de-anonymization study (Narayanan & Shmatikov)](https://www.cs.utexas.edu/~shmat/shmat_oak08netflix.pdf) - Why naive anonymization fails: re-identifying users in an "anonymized" dataset.

## Related Awesome Lists

- [Awesome Privacy](https://github.com/Lissy93/awesome-privacy) - Consumer-facing privacy-respecting apps and services.
- [Awesome Anonymization for LLMs](https://github.com/malteos/awesome-anonymization-for-llms) - LLM-specific anonymization resources.
- [Awesome Synthetic Data](https://github.com/gretelai/awesome-synthetic-data) - Synthetic data tools, open source and commercial.

## Contributing

Contributions welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first. In short: open source preferred, actively maintained, one-line description, alphabetical-ish within category.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the authors have waived all copyright and related rights to this work.
