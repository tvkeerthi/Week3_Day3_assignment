Automates cleaning of student_enrollment_raw.csv (50 rows) using an LLM, then routes each row into a Google Sheet tab based on City + Email validity.

Workflow
Form Trigger → Extract from File → Loop Over Items
  → Basic LLM Chain (cleans row) → Code node (parses JSON)
  → Wait (2s, avoids Sheets rate limit)
  → IF City=="Chennai"
       ├─ true  → IF1 Email valid? → chennai_valid_email / chennai_invalid_email
       └─ false → IF2 Email valid? → other_valid_email / other_invalid_email
Cleaning rules

Name→Title Case · Email validated (@ + .com/.in) · Phone→digits only (10+) · Course→canonical name · Fee_Paid→boolean · City→Title Case ("UNKNOWN" if blank) · Date→YYYY-MM-DD.
