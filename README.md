# task-5
import java.util.*;

class Patient {
    int id;
    String name;
    int age;
    String disease;

    Patient(int id, String name, int age, String disease) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.disease = disease;
    }
}

class Appointment {
    int patientId;
    String doctorName;
    String date;

    Appointment(int patientId, String doctorName, String date) {
        this.patientId = patientId;
        this.doctorName = doctorName;
        this.date = date;
    }
}

class Donor {
    String name;
    String bloodGroup;

    Donor(String name, String bloodGroup) {
        this.name = name;
        this.bloodGroup = bloodGroup;
    }
}

public class MedicalManagementSystem {

    static ArrayList<Patient> patients = new ArrayList<>();
    static ArrayList<Appointment> appointments = new ArrayList<>();
    static ArrayList<Donor> donors = new ArrayList<>();

    static Scanner sc = new Scanner(System.in);
    static int patientIdCounter = 1;

    public static void main(String[] args) {

        // Default donors
        donors.add(new Donor("Ravi", "O+"));
        donors.add(new Donor("Sita", "A+"));

        System.out.println("===== Medical Management System =====");

        login();

        int choice;

        do {

            System.out.println("\n1. Add Patient");
            System.out.println("2. View Patients");
            System.out.println("3. Book Appointment");
            System.out.println("4. View Appointments");
            System.out.println("5. Blood Donor List");
            System.out.println("6. Exit");

            System.out.print("Enter choice: ");
            choice = sc.nextInt();

            switch (choice) {

                case 1:
                    addPatient();
                    break;

                case 2:
                    viewPatients();
                    break;

                case 3:
                    bookAppointment();
                    break;

                case 4:
                    viewAppointments();
                    break;

                case 5:
                    viewDonors();
                    break;

                case 6:
                    System.out.println("Exiting system...");
                    break;

                default:
                    System.out.println("Invalid choice");
            }

        } while (choice != 6);
    }

    static void login() {

        String username, password;

        System.out.print("Username: ");
        username = sc.next();

        System.out.print("Password: ");
        password = sc.next();

        if (username.equals("admin") && password.equals("1234")) {
            System.out.println("Login Successful!");
        } else {
            System.out.println("Invalid Login! Exiting...");
            System.exit(0);
        }
    }

    static void addPatient() {

        sc.nextLine();

        System.out.print("Enter Patient Name: ");
        String name = sc.nextLine();

        System.out.print("Enter Age: ");
        int age = sc.nextInt();

        sc.nextLine();

        System.out.print("Enter Disease: ");
        String disease = sc.nextLine();

        Patient p = new Patient(patientIdCounter++, name, age, disease);
        patients.add(p);

        System.out.println("Patient added successfully!");
    }

    static void viewPatients() {

        System.out.println("\n--- Patient Records ---");

        for (Patient p : patients) {
            System.out.println("ID: " + p.id +
                    " Name: " + p.name +
                    " Age: " + p.age +
                    " Disease: " + p.disease);
        }

        if (patients.isEmpty()) {
            System.out.println("No patients found.");
        }
    }

    static void bookAppointment() {

        System.out.print("Enter Patient ID: ");
        int id = sc.nextInt();

        sc.nextLine();

        System.out.print("Enter Doctor Name: ");
        String doctor = sc.nextLine();

        System.out.print("Enter Appointment Date: ");
        String date = sc.nextLine();

        appointments.add(new Appointment(id, doctor, date));

        System.out.println("Appointment booked successfully!");
    }

    static void viewAppointments() {

        System.out.println("\n--- Appointment List ---");

        for (Appointment a : appointments) {

            System.out.println("Patient ID: " + a.patientId +
                    " Doctor: " + a.doctorName +
                    " Date: " + a.date);
        }

        if (appointments.isEmpty()) {
            System.out.println("No appointments scheduled.");
        }
    }

    static void viewDonors() {

        System.out.println("\n--- Blood Donors ---");

        for (Donor d : donors) {
            System.out.println("Name: " + d.name +
                    " Blood Group: " + d.bloodGroup);
        }
    }
}
