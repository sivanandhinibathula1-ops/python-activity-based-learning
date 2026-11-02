1. Problem Statement
Design and develop a Python-based University Scholarship Allocation System that evaluates student applications based on aggregate marks, subject-wise minimum marks, attendance percentage and annual family income.

The system should identify eligible students, rank them according to their academic performance, resolve ties using predefined rules and allocate scholarships based on the available number of seats.

The tie-breaking rules are:

Higher aggregate marks.

Higher attendance percentage.

Lower annual family income.

Higher marks in Subject 1.

2. Algorithm
Start the program.

Set the eligibility criteria:

Minimum aggregate marks = 75%.

Minimum subject marks = 60%.

Minimum attendance = 75%.

Maximum annual family income = ₹2,50,000.

Enter the number of students.

Enter student details such as roll number, name, subject marks, attendance and annual family income.

Calculate the aggregate percentage.

Check all eligibility conditions.

If the student does not satisfy the conditions, reject the application.

If the student satisfies all conditions, add the student to the eligible list.

Rank eligible students based on aggregate marks.

Resolve ties using attendance, family income and Subject 1 marks.

Check the available scholarship seats.

Allocate scholarships to the top-ranking students.

Display the eligible students, ranks and scholarship status.

Stop the program.

3.  Flowchart
This is the flowchart with proper symbols, boxes, decision diamonds, input/output symbols and connecting arrows.


mermaid

flowchart TD
    A([START])
    B[/Student Registration/]
    C[Enter Student Details]
    D[/Enter Subject Marks, Attendance and Income/]
    E[Calculate Aggregate Percentage]
    F{Eligibility Check}
    G[Reject Application]
    H[Add to Eligible Students List]
    I[Rank Eligible Students]
    J{Same Aggregate Marks?}
    K[Apply Tie Breaking Rules]
    L[Check Available Scholarship Seats]
    M[Allocate Scholarship]
    N[/Display Selected Students, Rank and Status/]
    O([STOP])

    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
    F -->|No| G
    F -->|Yes| H
    G --> O
    H --> I
    I --> J
    J -->|Yes| K
    J -->|No| L
    K --> L
    L --> M
    M --> N
    N --> O
Flowchart Symbols
Symbol

Meaning

Oval

Start / Stop

Rectangle

Processing

Parallelogram

Input / Output

Diamond

Decision

Arrow

Flow direction

4. Python Source Code

python

# University Scholarship Allocation System

# Eligibility Criteria
MIN_AGGREGATE = 75
MIN_SUBJECT_MARKS = 60
MIN_ATTENDANCE = 75
MAX_INCOME = 250000

# Number of scholarships available
SCHOLARSHIP_SEATS = 3

students = []
eligible_students = []

# Input number of students
n = int(input("Enter number of students: "))

# Collect student details
for i in range(n):

    print("\nEnter details of Student", i + 1)

    roll_no = input("Enter Roll Number: ")
    name = input("Enter Student Name: ")

    m1 = float(input("Enter Subject 1 Marks: "))
    m2 = float(input("Enter Subject 2 Marks: "))
    m3 = float(input("Enter Subject 3 Marks: "))

    attendance = float(input("Enter Attendance Percentage: "))
    income = float(input("Enter Annual Family Income: "))

    # Calculate aggregate percentage
    aggregate = (m1 + m2 + m3) / 3

    # Store student details
    student = {
        "roll_no": roll_no,
        "name": name,
        "m1": m1,
        "m2": m2,
        "m3": m3,
        "attendance": attendance,
        "income": income,
        "aggregate": aggregate
    }

    students.append(student)

    # Check eligibility
    if (aggregate >= MIN_AGGREGATE and
        m1 >= MIN_SUBJECT_MARKS and
        m2 >= MIN_SUBJECT_MARKS and
        m3 >= MIN_SUBJECT_MARKS and
        attendance >= MIN_ATTENDANCE and
        income <= MAX_INCOME):

        eligible_students.append(student)

# Sort eligible students
# Tie-breaking rules:
# 1. Higher aggregate
# 2. Higher attendance
# 3. Lower family income
# 4. Higher marks in Subject 1

eligible_students.sort(
    key=lambda s: (
        -s["aggregate"],
        -s["attendance"],
        s["income"],
        -s["m1"]
    )
)

# Display eligible students
print("\n========== ELIGIBLE STUDENTS ==========")

if len(eligible_students) == 0:

    print("No students are eligible for scholarship.")

else:

    print("\nRank  Roll No  Name  Aggregate  Attendance  Income  Status")

    for rank, s in enumerate(eligible_students, start=1):

        if rank <= SCHOLARSHIP_SEATS:
            status = "Scholarship Awarded"
        else:
            status = "Eligible - Not Selected"

        print(
            rank,
            s["roll_no"],
            s["name"],
            round(s["aggregate"], 2),
            s["attendance"],
            s["income"],
            status
        )

# Display summary
print("\n========== SUMMARY ==========")

print("Total Students:", n)
print("Eligible Students:", len(eligible_students))
print("Scholarships Available:", SCHOLARSHIP_SEATS)

print("Scholarships Awarded:",
      min(len(eligible_students), SCHOLARSHIP_SEATS))

print("\n========== PROGRAM COMPLETED ==========")
5. Source Input
Sample input for five students:


text
Enter number of students: 5

Enter details of Student 1
Roll Number: 101
Student Name: Arun
Subject 1 Marks: 90
Subject 2 Marks: 85
Subject 3 Marks: 80
Attendance Percentage: 90
Annual Family Income: 180000

Enter details of Student 2
Roll Number: 102
Student Name: Banu
Subject 1 Marks: 85
Subject 2 Marks: 80
Subject 3 Marks: 85
Attendance Percentage: 95
Annual Family Income: 200000

Enter details of Student 3
Roll Number: 103
Student Name: Charan
Subject 1 Marks: 70
Subject 2 Marks: 75
Subject 3 Marks: 80
Attendance Percentage: 85
Annual Family Income: 150000

Enter details of Student 4
Roll Number: 104
Student Name: Divya
Subject 1 Marks: 95
Subject 2 Marks: 90
Subject 3 Marks: 95
Attendance Percentage: 92
Annual Family Income: 220000

Enter details of Student 5
Roll Number: 105
Student Name: Esha
Subject 1 Marks: 80
Subject 2 Marks: 82
Subject 3 Marks: 78
Attendance Percentage: 88
Annual Family Income: 240000
6. Source Output

text
========== ELIGIBLE STUDENTS ==========

Rank  Roll No  Name   Aggregate  Attendance  Income  Status

1     104      Divya    93.33       92        220000
Scholarship Awarded

2     101      Arun     85.00       90        180000
Scholarship Awarded

3     102      Banu     83.33       95        200000
Scholarship Awarded

4     105      Esha     80.00       88        240000
Eligible - Not Selected

========== SUMMARY ==========

Total Students: 5
Eligible Students: 4
Scholarships Available: 3
Scholarships Awarded: 3

========== PROGRAM COMPLETED ==========
