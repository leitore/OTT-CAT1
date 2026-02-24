# OTT-CAT1
from datetime import datetime, date, time
class User:
    def __init__(self, user_id, username, password, role):
        self.__user_id = user_id            # Encapsulation (private)
        self.__username = username
        self.__password = password
        self.__role = role
        self.__last_login = None
        self.__is_active = True

    # Getter method
    def get_username(self):
        return self.__username

    def login(self):
        self.__last_login = datetime.now()
        print(f"{self.__username} logged in at {self.__last_login}")

    def logout(self):
        print(f"{self.__username} logged out.")
        class Patient(User):
    def __init__(self, user_id, username, password, patient_id, date_of_birth):
        super().__init__(user_id, username, password, "Patient")
        self.__patient_id = patient_id
        self.__date_of_birth = date_of_birth

    def calculate_age(self):
        today = date.today()
        return today.year - self.__date_of_birth.year

class HealthcareProvider(User):
    def __init__(self, user_id, username, password, provider_id, specialization):
        super().__init__(user_id, username, password, "Provider")
        self.__provider_id = provider_id
        self.__specialization = specialization

    # Polymorphism (Method Overriding)
    def login(self):
        print(f"Dr. {self.get_username()} logged in with elevated privileges.")

class Appointment:
    def __init__(self, appointment_id, appointment_date, appointment_time, patient, provider):
        self.__appointment_id = appointment_id
        self.__date = appointment_date
        self.__time = appointment_time
        self.__patient = patient          # Association
        self.__provider = provider        # Association

    def schedule_appointment(self):
        print("Appointment Scheduled:")
        print(f"Patient: {self.__patient.get_username()}")
        print(f"Provider: Dr. {self.__provider.get_username()}")
        print(f"Date: {self.__date} Time: {self.__time}")

class Bill:
    def __init__(self, bill_id, amount):
        self.__bill_id = bill_id
        self.__amount = amount
        self.__status = "Pending"

    def get_amount(self):
        return self.__amount

    def get_status(self):
        return self.__status

    def mark_as_paid(self):
        self.__status = "Paid"

class Payment:
    def __init__(self, payment_id, amount):
        self.__payment_id = payment_id
        self.__amount = amount
        self.__payment_date = date.today()

    def process_payment(self, bill):
        if self.__amount >= bill.get_amount():
            bill.mark_as_paid()
            print("Payment Successful. Bill marked as Paid.")
        else:
            print("Insufficient payment amount.")

print("===== MHC-PMS SYSTEM START =====\n")

# Create Patient
patient = Patient(
    "U001",
    "PaulGitonga",
    "1234",
    "P001",
    date(2000, 5, 20)
)

patient.login()
print("Patient Age:", patient.calculate_age())
print()

# Create Healthcare Provider
provider = HealthcareProvider(
    "U002",
    "DrJohn",
    "abcd",
    "H001",
    "Psychiatry"
)

provider.login()
print()

# Schedule Appointment
appointment = Appointment(
    "A001",
    date.today(),
    time(10, 30),
    patient,
    provider
)

appointment.schedule_appointment()
print()

# Generate Bill
bill = Bill("B001", 9000.00)
print("Bill Generated: Ksh", bill.get_amount())
print("Bill Status:", bill.get_status())
print()

# Process Payment
payment = Payment("PAY001", 9000.00)
payment.process_payment(bill)

print("Updated Bill Status:", bill.get_status())
print()

patient.logout()

print("\n===== SYSTEM END =====")

===== MHC-PMS SYSTEM START =====

PaulGitonga logged in at 2026-02-19 22:19:27.724102
Patient Age: 26

Dr. DrJohn logged in with elevated privileges.

Appointment Scheduled:
Patient: PaulGitonga
Provider: Dr. DrJohn
Date: 2026-02-19 Time: 10:30:00

Bill Generated: Ksh 9000.0
Bill Status: Pending

Payment Successful. Bill marked as Paid.
Updated Bill Status: Paid

PaulGitonga logged out.

===== SYSTEM END =====

 



        
