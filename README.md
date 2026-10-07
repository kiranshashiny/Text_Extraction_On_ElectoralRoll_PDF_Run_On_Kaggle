# Text_Extraction_On_ElectoralRoll_PDF_Run_On_Kaggle



<img width="838" height="268" alt="image" src="https://github.com/user-attachments/assets/3c99e931-df74-4e4d-aff4-6cda946890c1" />



<img width="257" height="368" alt="image" src="https://github.com/user-attachments/assets/06561d7a-e19b-42cc-a6bb-6d08cf7c9c53" />

```


import os
import glob
import subprocess

# ==========================================
# STEP 1: Install System Dependencies & Libs
# ==========================================
print("Installing poppler-utils and pdf2image...")
# poppler-utils provides pdftoppm, which powers pdf2image
subprocess.run("apt-get update -y > /dev/null", shell=True)
subprocess.run("apt-get install -y poppler-utils > /dev/null", shell=True)
subprocess.run("pip install -q pdf2image Pillow", shell=True)

from pdf2image import convert_from_path

# ==========================================
# STEP 2: Auto-Detect Input PDF
# ==========================================
# Look recursively for any .pdf file inside /kaggle/input/
pdf_files = glob.glob("/kaggle/input/**/*.pdf", recursive=True)

if not pdf_files:
    raise FileNotFoundError("No PDF file found in /kaggle/input/. Make sure your dataset is attached to the notebook.")

PDF_PATH = pdf_files[0]
OUTPUT_DIR = "/kaggle/working/png_pages"
os.makedirs(OUTPUT_DIR, exist_ok=True)

print(f"Found input PDF: {PDF_PATH}")
print(f"Extracting PNG files to: {OUTPUT_DIR}")

# ==========================================
# STEP 3: Convert PDF Pages into PNG Files
# ==========================================
# dpi=300 ensures clean text rendering for vision processing
images = convert_from_path(PDF_PATH, dpi=300)

generated_files = []
for idx, image in enumerate(images, start=1):
    output_filename = f"page_{idx:03d}.png"
    output_path = os.path.join(OUTPUT_DIR, output_filename)
    
    # Save as PNG
    image.save(output_path, "PNG")
    generated_files.append(output_path)
    print(f"Saved: {output_filename}")

print(f"\nSuccessfully chopped PDF into {len(generated_files)} PNG images!")

```


Parse each page

```
import os
import glob
import subprocess

# ==========================================
# STEP 1: Install System Dependencies & Libs
# ==========================================
print("Installing poppler-utils and pdf2image...")
# poppler-utils provides pdftoppm, which powers pdf2image
subprocess.run("apt-get update -y > /dev/null", shell=True)
subprocess.run("apt-get install -y poppler-utils > /dev/null", shell=True)
subprocess.run("pip install -q pdf2image Pillow", shell=True)

from pdf2image import convert_from_path

# ==========================================
# STEP 2: Auto-Detect Input PDF
# ==========================================
# Look recursively for any .pdf file inside /kaggle/input/
pdf_files = glob.glob("/kaggle/input/**/*.pdf", recursive=True)

if not pdf_files:
    raise FileNotFoundError("No PDF file found in /kaggle/input/. Make sure your dataset is attached to the notebook.")

PDF_PATH = pdf_files[0]
OUTPUT_DIR = "/kaggle/working/png_pages"
os.makedirs(OUTPUT_DIR, exist_ok=True)

print(f"Found input PDF: {PDF_PATH}")
print(f"Extracting PNG files to: {OUTPUT_DIR}")

# ==========================================
# STEP 3: Convert PDF Pages into PNG Files
# ==========================================
# dpi=300 ensures clean text rendering for vision processing
images = convert_from_path(PDF_PATH, dpi=300)

generated_files = []
for idx, image in enumerate(images, start=1):
    output_filename = f"page_{idx:03d}.png"
    output_path = os.path.join(OUTPUT_DIR, output_filename)
    
    # Save as PNG
    image.save(output_path, "PNG")
    generated_files.append(output_path)
    print(f"Saved: {output_filename}")

print(f"\nSuccessfully chopped PDF into {len(generated_files)} PNG images!")

```


<img width="663" height="151" alt="image" src="https://github.com/user-attachments/assets/59cf7951-884f-40f8-80c4-1d42168cb275" />
