"""
Practical 1 - Data Privacy Audit
Organisation used as case study: Sunrise Retail Pvt Ltd (fictional e-commerce store)

Idea: an auditor walks through a checklist of controls that every company
handling customer data SHOULD have. Each item is scored, and we work out
an overall risk rating at the end. This mirrors how a real privacy audit
report looks (finding -> risk level -> recommendation).
"""

# each control is: (area, question, is_it_met, weight_out_of_10)
audit_checklist = [
    ("Data Inventory", "Does the company maintain a record of what personal data it collects?", True, 8),
    ("Data Inventory", "Is there a data flow map showing where data moves internally/externally?", False, 7),
    ("Consent", "Is consent taken before collecting data from customers?", True, 9),
    ("Consent", "Can customers withdraw consent easily?", False, 6),
    ("Access Control", "Is customer data access restricted by role (RBAC)?", True, 9),
    ("Access Control", "Are admin accounts protected with MFA?", False, 8),
    ("Storage", "Is sensitive data (passwords, card info) encrypted at rest?", True, 10),
    ("Storage", "Is there a data retention/deletion policy in place?", False, 7),
    ("Third Parties", "Are vendor contracts checked for data protection clauses?", False, 6),
    ("Incident Handling", "Is there a documented breach response plan?", False, 9),
]


def calculate_risk_score(checklist):
    total_weight = sum(item[3] for item in checklist)
    achieved_weight = sum(item[3] for item in checklist if item[2])
    # risk % is basically "how much of the required protection is missing"
    risk_percent = round(100 - (achieved_weight / total_weight * 100), 1)
    return risk_percent


def classify_risk(risk_percent):
    if risk_percent < 20:
        return "Low"
    elif risk_percent < 50:
        return "Medium"
    else:
        return "High"


def print_audit_report(company_name, checklist):
    print(f"Data Privacy Audit Report - {company_name}")
    print("-" * 55)

    findings_failed = []
    for area, question, met, weight in checklist:
        status = "PASS" if met else "GAP"
        print(f"[{status}] ({area}) {question}")
        if not met:
            findings_failed.append((area, question, weight))

    risk = calculate_risk_score(checklist)
    risk_level = classify_risk(risk)

    print("-" * 55)
    print(f"Overall risk score: {risk}%  ->  Risk level: {risk_level}")
    print("\nTop recommendations (highest weight gaps first):")

    # sort the failed items so the most serious gaps show up first
    findings_failed.sort(key=lambda x: x[2], reverse=True)
    for area, question, weight in findings_failed[:3]:
        print(f" - Fix: {question}  (Area: {area}, Priority weight: {weight})")


if __name__ == "__main__":
    print_audit_report("Sunrise Retail Pvt Ltd", audit_checklist)
