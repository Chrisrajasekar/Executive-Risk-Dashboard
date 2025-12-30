# Executive-Risk-Dashboard
This project features an Executive Risk Dashboard built in Power BI, designed to automate the reporting and oversight of IT risk findings across a global enterprise. It serves as a centralized "Independent Review" layer, aggregating data from GRC tools like Archer to provide leadership with real-time visibility into the organization's risk posture.

# Visualization

![Executive Risk Dashboard](https://github.com/user-attachments/assets/3cae0e90-0afe-4eee-9e32-b6757818df83)


# 🎯 Strategic Alignment 
This tool was built to address specific requirements for the Senior IT Risk Analyst role, includes

**Cross-Regional Oversight**: Visualizes risk distribution across global teams to support regional risk management activities.

**Independent Review & Challenge**: Identifies "Risk Accepted" and "Overdue" findings, enabling analysts to hold application owners accountable for remediation.

**Regulatory Focus**: Specifically tracks findings related to NYDF 500, GDPR, and PCI DSS.

**Aging & Metrics**: Automates the tracking of remediation milestones and "High Risks Open > 90 Days," a key metric for senior leadership.

# 📊 Key Features

**Global Risk Heatmap** : A geographical visualization showing risk concentration by severity (High, Medium, Low) across global business hubs.

**High Severity Aging Analysis**: A prioritized bar chart highlighting findings that have remained open beyond 90 days, facilitating targeted follow-ups.

**Status Distribution**: A high-level view of "Open" vs. "Closed" findings to measure remediation efficiency and audit readiness.

**KRI Reporting**: Displays total risk counts and severity breakdowns to act as a Key Risk Indicator (KRI) dashboard for executive-level communications

# 🛠️ Technical Stack

**Data Source**: Custom CSV dataset simulating mock IT risk findings (Vulnerabilities, DLP exceptions, NPID exposure, and Access Control gaps).

**Visualization Tool**: Power BI Desktop.

**Analytical Logic**: Utilizes DAX for aging calculations and regional slicing to support integrated risk profiles (IRP).

# 📁 Repository Contents
**Executive_Risk_Dashboard.pbix**: The core Power BI project file.

**Mock_Risk_Findings.csv**: The underlying dataset featuring global risk data.

**Dashboard_Preview.png**: A high-resolution screenshot of the final report.

**Python Data Generator Script** file named generate_risk_data.py. This script will generate the CSV file to be used for Power BI dashboard.

import pandas as pd
import random
from datetime import datetime, timedelta

def generate_mock_risk_data(num_records=20):
    regions = ['UK', 'Toronto', 'India', 'USA']
    severities = ['High', 'Medium', 'Low']
    statuses = ['Open', 'Closed', 'Risk Accepted']
    categories = [
        'Vulnerability Mgmt', 'Data Privacy (NPID)', 'Access Control (NYDF)', 
        'Identity & Access Mgmt', 'Third Party Risk', 'Regulatory (GDPR)', 'Encryption'
    ]
    owners = ['Server Ops', 'IAM Team', 'Cloud Security', 'App Dev', 'DB Admins']

    data = []
    
    for i in range(1, num_records + 1):
        # Generate a random due date (some in the past, some in the future)
        days_offset = random.randint(-60, 120)
        due_date = (datetime.now() + timedelta(days=days_offset)).strftime('%Y-%m-%d')
        
        data.append({
            'Risk_ID': f'R-{i:03}',
            'Title': f'Sample IT Risk Finding {i}',
            'Region': random.choice(regions),
            'Severity': random.choice(severities),
            'Status': random.choice(statuses),
            'Due_Date': due_date,
            'Owner': random.choice(owners),
            'Risk_Category': random.choice(categories)
        })

    df = pd.DataFrame(data)
    df.to_csv('risk_findings_mock_data.csv', index=False)
    print(f"Successfully generated {num_records} risk records to 'risk_findings_mock_data.csv'")

if __name__ == "__main__":
    generate_mock_risk_data(50) # Generates 50 rows of data

