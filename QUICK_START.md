# E-KYC Quick Start Guide

## ✅ Setup Status

### Completed Steps:
1. ✓ All required Python packages installed
2. ✓ Configuration files created
3. ✓ Database setup script created
4. ✓ Code issues fixed (debugging code removed, unused connections cleaned)

### Next Steps to Run the Application:

#### 1. Configure Database (REQUIRED)
Edit `config.toml` and update with your MySQL credentials:
```toml
[database]
user = "your_mysql_username"        # Change this
password = "your_mysql_password"    # Change this
host = "localhost"
database = "ekyc"
```

#### 2. Setup MySQL Database
Make sure MySQL server is running, then run:
```bash
python setup_database.py
```
This will create the database and required tables.

#### 3. Run the Application
```bash
streamlit run app.py
```

The application will open in your browser at `http://localhost:8501`

## Project Overview

This E-KYC application processes ID cards (PAN and Aadhar) by:
1. **Extracting ID card** from uploaded image
2. **Detecting face** in the ID card
3. **Verifying face** matches uploaded face image
4. **Extracting text** using OCR (EasyOCR)
5. **Parsing information** (Name, ID, DOB, etc.)
6. **Storing in database** with face embeddings for duplicate detection

## File Structure

- `app.py` - Main Streamlit application
- `preprocess.py` - Image preprocessing
- `ocr_engine.py` - Text extraction
- `postprocess.py` - Information parsing
- `face_verification.py` - Face detection and verification
- `sql_connection.py` - Database operations
- `setup_database.py` - Database setup script
- `config.toml` - Database configuration (UPDATE THIS!)
- `config.yaml` - Application configuration

## Troubleshooting

### Database Connection Error
- Ensure MySQL server is running
- Check credentials in `config.toml`
- Run `python setup_database.py` to create tables

### Face Detection Issues
- Ensure `data/models/haarcascade_frontalface_default.xml` exists
- Check image formats (JPG, PNG supported)

### Package Import Errors
- Run `python test_imports.py` to verify all packages
- Install missing packages: `pip install -r requirements.txt`

## Notes

- ID numbers are hashed (SHA-256) before storage for security
- Face embeddings are stored for duplicate detection
- Logs are stored in `logs/` directory
- Processed images stored in `data/02_intermediate_data/`

## Testing

To test if all packages are installed:
```bash
python test_imports.py
```

All packages should show `[OK]` status.

