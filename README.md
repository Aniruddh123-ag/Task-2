# Task-2
Automated Report Generation
<br>
import pandas as pd
<br> 
from fpdf import FPDF
<br>

def generate_report(input_file, output_pdf):
    """
    <br>
    Reads data from an input file, analyzes it (simple example),
    <br>
    and generates a formatted PDF report.
    """
    <br>
    try:
    <br>
 # 1. Read data from a file (e.g., CSV)
        df = pd.read_csv(input_file)
 # 2. Analyze data (simple example: calculate mean of a numeric column)
        if 'Value' in df.columns:
            mean_value = df['Value'].mean()
        else:
            mean_value = "N/A (No 'Value' column found)"
 # 3. Generate a formatted PDF report using FPDF
        pdf = FPDF()
        pdf.add_page()
        pdf.set_font("Arial", size=12)

        pdf.cell(200, 10, txt="Data Analysis Report", ln=True, align="C")
        pdf.cell(200, 10, txt="", ln=True) # Spacer

        pdf.cell(200, 10, txt=f"Input File: {input_file}", ln=True)
        pdf.cell(200, 10, txt=f"Number of rows: {len(df)}", ln=True)
        pdf.cell(200, 10, txt=f"Mean of 'Value' column: {mean_value}", ln=True)

        pdf.output(output_pdf)
        print(f"Report generated successfully: {output_pdf}")

    except FileNotFoundError:
        print(f"Error: Input file '{input_file}' not found.")
    except Exception as e:
        print(f"An error occurred: {e}")
# Example Usage:
# Create a dummy CSV file for testing
with open("sample_data.csv", "w") as f:
    f.write("Name,Value,Category\n")
    f.write("A,10,X\n")
    f.write("B,20,Y\n")
    f.write("C,15,X\n")

generate_report("sample_data.csv", "sample_report.pdf")
