[Upload ID Card] → preprocess.py → OCR (EasyOCR) → extract_text
       ↓
[Upload Selfie] → face_verification.py → DeepFace → verify match
       ↓
[Match?] → YES → sql_connection.py → store in MySQL
       ↓
Streamlit → Displays extracted info & verification result