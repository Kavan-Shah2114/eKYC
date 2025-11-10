# E-KYC Project Setup Guide

## Overview
This is an E-KYC (Electronic Know Your Customer) application that processes ID cards (PAN and Aadhar) using:
- Face verification (Haarcascade + DeepFace)
- OCR (EasyOCR) for text extraction
- MySQL database for storage
- Streamlit web interface

## Prerequisites
- Python 3.8+ (Currently using Python 3.12.4)
- MySQL Server installed and running
- Anaconda/Miniconda (optional but recommended)

## Setup Steps

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Configure Database
1. Copy the example config file:
   ```bash
   copy config.toml.example config.toml
   ```

2. Edit `config.toml` with your MySQL credentials:
   ```toml
   [database]
   user = "your_mysql_username"
   password = "your_mysql_password"
   host = "localhost"
   database = "ekyc"
   ```

### 3. Setup Database
Run the database setup script to create the required tables:
```bash
python setup_database.py
```

This will create:
- Database: `ekyc` (or your specified database name)
- Table: `users` (for PAN card data)
- Table: `aadhar` (for Aadhar card data)

### 4. Run the Application
```bash
streamlit run app.py
```

The application will open in your default web browser at `http://localhost:8501`

## Project Structure
- `app.py` - Main Streamlit application
- `preprocess.py` - Image preprocessing and ID card extraction
- `ocr_engine.py` - Text extraction using EasyOCR
- `postprocess.py` - Information extraction from OCR text
- `face_verification.py` - Face detection and verification
- `sql_connection.py` - Database operations
- `utils.py` - Utility functions
- `config.yaml` - Configuration for artifacts
- `config.toml` - Database configuration (create from config.toml.example)
- `setup_database.py` - Database setup script

## Features
1. **Face Verification**: Verifies that the face in the ID card matches the uploaded face image
2. **OCR Processing**: Extracts text from ID cards using EasyOCR
3. **Data Extraction**: Parses PAN/Aadhar information from extracted text
4. **Database Storage**: Stores user data with face embeddings for duplicate detection
5. **Duplicate Detection**: Checks if a user already exists in the database

## Troubleshooting

### Database Connection Issues
- Ensure MySQL server is running
- Check credentials in `config.toml`
- Verify database exists and tables are created

### Missing Dependencies
- Run `pip install -r requirements.txt`
- For EasyOCR, ensure you have the required system dependencies

### Face Detection Issues
- Ensure `data/models/haarcascade_frontalface_default.xml` exists
- Check that images are in supported formats (JPG, PNG, etc.)

## Notes
- The application uses SHA-256 hashing for ID numbers before storage
- Face embeddings are stored as text in the database
- Logs are stored in the `logs` directory
- Intermediate processed images are stored in `data/02_intermediate_data`

