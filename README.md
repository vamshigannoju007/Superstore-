##Encoding issue during ingestion

The source CSV was originally saved in a Windows legacy encoding (WIN1252).

PostgreSQL database encoding is UTF-8, so COPY/\copy must convert input text to UTF-8.

Import failed due to invalid byte sequences (example: byte 0x9D), which occur with Windows “smart quotes” and other punctuation.

##Fix: converted the CSV to UTF-8 (Notepad++: Encoding → Convert to UTF-8), then reloaded successfully.

##Lesson

Always validate file encoding before ingestion.

Standardize input files to UTF-8 to ensure consistent loading and correct text rendering.
