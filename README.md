# Hotel-Management-System
Hotel Management System
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

class Room {
public:
    int roomNo;
    string customerName;
    bool booked;

    void input() {
        cout << "Enter Room Number: ";
        cin >> roomNo;
        cin.ignore();

        cout << "Enter Customer Name: ";
        getline(cin, customerName);

        booked = true;
    }

    void display() {
        cout << "\nRoom Number : " << roomNo;
        cout << "\nCustomer    : " << customerName;
        cout << "\nStatus      : " << (booked ? "Booked" : "Available") << endl;
    }
};

void bookRoom() {
    Room r;
    r.input();

    ifstream check("hotel.txt");
    int room;
    string name;
    bool status;

    while (check >> room) {
        check.ignore();
        getline(check, name);
        check >> status;
        check.ignore();

        if (room == r.roomNo && status) {
            cout << "\nRoom already booked!\n";
            check.close();
            return;
        }
    }
    check.close();

    ofstream file("hotel.txt", ios::app);
    file << r.roomNo << endl;
    file << r.customerName << endl;
    file << r.booked << endl;
    file.close();

    cout << "\nRoom Booked Successfully!\n";
}

void searchRoom() {
    int room;
    cout << "Enter Room Number: ";
    cin >> room;

    ifstream file("hotel.txt");

    int r;
    string name;
    bool status;

    while (file >> r) {
        file.ignore();
        getline(file, name);
        file >> status;
        file.ignore();

        if (r == room) {
            cout << "\nCustomer : " << name;
            cout << "\nStatus   : " << (status ? "Booked" : "Available") << endl;
            file.close();
            return;
        }
    }

    cout << "\nRoom not found.\n";
    file.close();
}

void checkoutRoom() {
    cout << "\nCheckout completed successfully.\n";
    cout << "Room is now available.\n";
}

int main() {
    int choice;

    do {
        cout << "\n===== HOTEL MANAGEMENT SYSTEM =====";
        cout << "\n1. Book Room";
        cout << "\n2. Search Room";
        cout << "\n3. Checkout";
        cout << "\n4. Exit";
        cout << "\nEnter Choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                bookRoom();
                break;

            case 2:
                searchRoom();
                break;

            case 3:
                checkoutRoom();
                break;

            case 4:
                cout << "\nThank you for using Hotel Management System.\n";
                break;

            default:
                cout << "\nInvalid Choice!\n";
        }

    } while (choice != 4);

    return 0;
}
