"""
Patient Record Management System
PROG211 - Object-Oriented Programming 1
Health domain demonstration project.

Educational prototype only. Uses fictional sample records and in-memory storage.
It is not intended for real clinical use.
"""

class Patient:
    """Represents one fictional patient record."""

    def __init__(self, patient_id, name, age, visit_reason):
        self.patient_id = patient_id.strip()
        self.name = name.strip()
        self.age = age
        self.visit_reason = visit_reason.strip()

    def display_info(self):
        """Instance method: display this patient's details."""
        print(f"Patient ID: {self.patient_id}")
        print(f"Name: {self.name}")
        print(f"Age: {self.age}")
        print(f"Visit reason: {self.visit_reason}")

    def update_record(self, name=None, age=None, visit_reason=None):
        """Instance method: update supplied fields on this patient object."""
        if name is not None and name.strip():
            self.name = name.strip()
        if age is not None:
            if not self.is_valid_age(age):
                raise ValueError("Age must be between 0 and 120.")
            self.age = age
        if visit_reason is not None and visit_reason.strip():
            self.visit_reason = visit_reason.strip()

    @classmethod
    def create_demo_patient(cls):
        """Class method: create a fictional example using the class itself."""
        return cls("DEMO001", "Demo Patient", 30, "Routine check-up")

    @staticmethod
    def is_valid_age(age):
        """Static method: validate an age without needing an object."""
        return isinstance(age, int) and 0 <= age <= 120


class PatientManager:
    """Stores and manages Patient objects in a Python list."""

    def __init__(self):
        self.patients = []

    def add_patient(self, patient):
        """Add a Patient object if its ID is not already in use."""
        if not isinstance(patient, Patient):
            raise TypeError("Only Patient objects can be added.")
        if self.find_patient(patient.patient_id) is not None:
            raise ValueError("A patient with that ID already exists.")
        self.patients.append(patient)

    def find_patient(self, patient_id):
        """Return the matching patient, or None if no match exists."""
        patient_id = patient_id.strip().lower()
        for patient in self.patients:
            if patient.patient_id.lower() == patient_id:
                return patient
        return None

    def display_all_patients(self):
        """Display every patient currently stored in the list."""
        if not self.patients:
            print("\nNo patient records found.")
            return
        print("\n--- Patient Records ---")
        for patient in self.patients:
            print("-" * 28)
            patient.display_info()
        print("-" * 28)

    def update_patient(self, patient_id, name=None, age=None, visit_reason=None):
        """Find and update a patient; return True if found."""
        patient = self.find_patient(patient_id)
        if patient is None:
            return False
        patient.update_record(name=name, age=age, visit_reason=visit_reason)
        return True


def read_age(prompt="Age: "):
    """Read and validate an age from console input."""
    raw_age = input(prompt).strip()
    if not raw_age.isdigit():
        raise ValueError("Please enter age as a whole number.")
    age = int(raw_age)
    if not Patient.is_valid_age(age):
        raise ValueError("Age must be between 0 and 120.")
    return age


def add_patient_interactively(manager):
    """Collect fictional/demo details and add a patient record."""
    print("\nEnter fictional/demo patient details only.")
    patient_id = input("Patient ID: ").strip()
    name = input("Name: ").strip()
    if not patient_id or not name:
        print("Patient ID and name cannot be blank.")
        return
    try:
        age = read_age()
    except ValueError as error:
        print(f"Invalid age: {error}")
        return
    visit_reason = input("Visit reason: ").strip()
    if not visit_reason:
        print("Visit reason cannot be blank.")
        return
    try:
        manager.add_patient(Patient(patient_id, name, age, visit_reason))
        print("Patient record added successfully.")
    except (TypeError, ValueError) as error:
        print(f"Could not add record: {error}")


def update_patient_interactively(manager):
    """Prompt for a patient ID and update supplied fields."""
    patient_id = input("Enter patient ID to update: ").strip()
    patient = manager.find_patient(patient_id)
    if patient is None:
        print("Patient record not found.")
        return
    print("Leave a field blank to keep its current value.")
    name = input(f"Name [{patient.name}]: ").strip()
    age_text = input(f"Age [{patient.age}]: ").strip()
    visit_reason = input(f"Visit reason [{patient.visit_reason}]: ").strip()

    age = None
    if age_text:
        try:
            if not age_text.isdigit():
                raise ValueError("Age must be a whole number.")
            age = int(age_text)
            if not Patient.is_valid_age(age):
                raise ValueError("Age must be between 0 and 120.")
        except ValueError as error:
            print(f"Invalid age: {error}")
            return

    try:
        manager.update_patient(
            patient_id,
            name=name or None,
            age=age,
            visit_reason=visit_reason or None
        )
        print("Patient record updated successfully.")
    except ValueError as error:
        print(f"Could not update record: {error}")


def load_demo_records(manager):
    """Add clearly fictional records for a quick demonstration."""
    examples = [
        Patient("P001", "Amina Example", 24, "Routine consultation"),
        Patient("P002", "Kofi Sample", 41, "Follow-up visit"),
    ]
    for patient in examples:
        if manager.find_patient(patient.patient_id) is None:
            manager.add_patient(patient)


def main():
    manager = PatientManager()
    # The class method demonstrates creating an object through the class.
    manager.add_patient(Patient.create_demo_patient())

    menu = """
========================================
 PATIENT RECORD MANAGEMENT SYSTEM
 Educational prototype - fictional data
========================================
1. Add patient record
2. Display all records
3. Search for a patient
4. Update a patient record
5. Load extra demo records
0. Exit
"""

    while True:
        print(menu)
        choice = input("Choose an option: ").strip()

        if choice == "1":
            add_patient_interactively(manager)
        elif choice == "2":
            manager.display_all_patients()
        elif choice == "3":
            patient_id = input("Enter patient ID: ").strip()
            patient = manager.find_patient(patient_id)
            if patient:
                print()
                patient.display_info()
            else:
                print("Patient record not found.")
        elif choice == "4":
            update_patient_interactively(manager)
        elif choice == "5":
            load_demo_records(manager)
            print("Demo records loaded (fictional data only).")
        elif choice == "0":
            print("Exiting. Remember: do not enter real patient information.")
            break
        else:
            print("Invalid option. Choose 0, 1, 2, 3, 4, or 5.")


if __name__ == "__main__":
    main()