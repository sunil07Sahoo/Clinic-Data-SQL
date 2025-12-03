CREATE DATABASE healthcare_clinic;
USE healthcare_clinic;
-- 1. Patients table
CREATE TABLE patients (
    patient_id     INT PRIMARY KEY,
    first_name     VARCHAR(50),
    last_name      VARCHAR(50),
    gender         CHAR(1),
    date_of_birth  DATE,
    city           VARCHAR(50),
    phone          VARCHAR(15)
);

-- 2. Doctors table
CREATE TABLE doctors (
    doctor_id   INT PRIMARY KEY,
    full_name   VARCHAR(100),
    specialty   VARCHAR(50)
);

-- 3. Appointments table
CREATE TABLE appointments (
    appointment_id    INT PRIMARY KEY,
    patient_id        INT,
    doctor_id         INT,
    appointment_date  DATE,
    appointment_time  TIME,
    reason            VARCHAR(100),
    status            VARCHAR(20),   -- Scheduled, Completed, Cancelled
    FOREIGN KEY (patient_id) REFERENCES patients(patient_id),
    FOREIGN KEY (doctor_id)  REFERENCES doctors(doctor_id)
);

-- 4. Bills table
CREATE TABLE bills (
    bill_id         INT PRIMARY KEY,
    appointment_id  INT,
    bill_date       DATE,
    amount          DECIMAL(10,2),
    payment_status  VARCHAR(20),      -- Paid, Pending, Cancelled
    FOREIGN KEY (appointment_id) REFERENCES appointments(appointment_id)
);
INSERT INTO patients (patient_id, first_name, last_name, gender, date_of_birth, city, phone) VALUES
(1, 'Ravi',    'Sharma',   'M', '1985-03-10', 'Mumbai',   '9876500001'),
(2, 'Priya',   'Iyer',     'F', '1990-07-22', 'Chennai',  '9876500002'),
(3, 'Amit',    'Patel',    'M', '1978-11-05', 'Ahmedabad','9876500003'),
(4, 'Sneha',   'Reddy',    'F', '1995-01-15', 'Hyderabad','9876500004'),
(5, 'Rahul',   'Verma',    'M', '1982-09-09', 'Mumbai',   '9876500005'),
(6, 'Anita',   'Kulkarni', 'F', '1988-12-30', 'Pune',     '9876500006'),
(7, 'Karan',   'Singh',    'M', '2000-04-18', 'Delhi',    '9876500007'),
(8, 'Lakshmi', 'Nair',     'F', '1975-06-25', 'Kochi',    '9876500008');

INSERT INTO doctors (doctor_id, full_name, specialty) VALUES
(1, 'Dr. Meera Joshi',      'General Medicine'),
(2, 'Dr. Arjun Nair',       'Cardiology'),
(3, 'Dr. Kavita Deshmukh',  'Orthopedics'),
(4, 'Dr. Sanjay Rao',       'Dermatology');

INSERT INTO appointments (appointment_id, patient_id, doctor_id, appointment_date, appointment_time, reason, status) VALUES
(1,  1, 1, '2025-01-10', '10:00:00', 'Fever and headache',          'Completed'),
(2,  2, 2, '2025-01-11', '11:30:00', 'Chest pain',                  'Completed'),
(3,  3, 3, '2025-01-11', '15:00:00', 'Knee pain',                   'Completed'),
(4,  4, 1, '2025-01-12', '09:30:00', 'General checkup',             'Cancelled'),
(5,  5, 2, '2025-01-12', '16:00:00', 'Breathlessness',              'Completed'),
(6,  6, 4, '2025-01-13', '14:00:00', 'Skin rash',                   'Completed'),
(7,  7, 1, '2025-01-13', '10:30:00', 'Stomach pain',                'Scheduled'),
(8,  8, 3, '2025-01-14', '11:00:00', 'Back pain',                   'Completed'),
(9,  1, 2, '2025-01-15', '12:00:00', 'Follow-up for chest pain',    'Scheduled'),
(10, 2, 1, '2025-01-15', '09:00:00', 'Fever follow-up',             'Scheduled'),
(11, 3, 4, '2025-01-16', '13:00:00', 'Allergy check',               'Completed'),
(12, 4, 2, '2025-01-16', '15:30:00', 'High BP',                     'Completed'),
(13, 5, 3, '2025-01-17', '10:00:00', 'Shoulder pain',               'Cancelled'),
(14, 6, 2, '2025-01-17', '11:30:00', 'Heart checkup',               'Completed'),
(15, 7, 4, '2025-01-18', '16:00:00', 'Acne treatment',              'Scheduled');

INSERT INTO bills (bill_id, bill_date, appointment_id, amount, payment_status) VALUES
(1,  '2025-01-10', 4,  800.00,  'Paid'),
(2,  '2025-01-11', 2, 1500.00,  'Paid'),
(3,  '2025-01-11', 3, 1200.00,  'Pending'),
(4,  '2025-01-12', 5, 2000.00,  'Paid'),
(5,  '2025-01-13', 6,  900.00,  'Paid'),
(6,  '2025-01-14', 8, 1100.00,  'Pending'),
(7,  '2025-01-16',11,  700.00,  'Paid'),
(8,  '2025-01-16',12, 1600.00,  'Paid'),
(9,  '2025-01-17',14, 2200.00,  'Pending'),
(10, '2025-01-10', 1,  200.00,  'Paid');  -- lab charges extra

drop table bills;
drop table appointments;
SELECT * FROM patients;


