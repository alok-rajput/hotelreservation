# hotelreservation

#include <iostream>
#include <string>
#include <vector>
#include <fstream>

using namespace std;

struct Room {
 int id;
 bool booked;
 string type; // added room type (e.g., single, double, suite)
 double price; // added room price
};

struct Booking {
 string name;
 int roomID;
 string date; // added booking date
};

vector<Room> rooms;
vector<Booking> bookings;

// added user authentication
string username;
string password;

void showRooms() {
 for (const auto &room : rooms) {
  cout << "Room " << (link unavailable) << " (" << room.type << ") - $" << room.price << " " << (room.booked ? " (Booked)" : " (Available)") << endl;
 }
}

void bookRoom(int roomID, string name, string date) {
 for (auto &room : rooms) {
  if ((link unavailable) == roomID && !room.booked) {
   room.booked = true;
   bookings.push_back({name, roomID, date});
   cout << "Room " << roomID << " booked successfully!" << endl;
   return;
  }
 }
 cout << "Room " << roomID << " is not available." << endl;
}

void loadRooms() {
 ifstream file("rooms.txt");
 string line;
 while (getline(file, line)) {
  int id;
  string type;
  double price;
  sscanf(line.c_str(), "%d %s %lf", &id, &type, &price);
  rooms.push_back({id, false, type, price});
 }
}

void saveBookings() {
 ofstream file("bookings.txt");
 for (const auto &booking : bookings) {
  file << booking.name << " " << booking.roomID << " " << booking.date << endl;
 }
}

void login() {
 cout << "Enter username: ";
 cin >> username;
 cout << "Enter password: ";
 cin >> password;
 if (username == "admin" && password == "password") {
  cout << "Login successful!" << endl;
 } else {
  cout << "Invalid credentials." << endl;
  exit(1);
 }
}

int main() {
 loadRooms();
 login();
 int choice;
 while (true) {
  cout << "1. Show Rooms\n2. Book Room\n3. View Bookings\n4. Exit" << endl;
  cin >> choice;
  switch (choice) {
   case 1:
    showRooms();
    break;
   case 2: {
    int roomID;
    string name;
    string date;
    cout << "Enter room ID: ";
    cin >> roomID;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Enter booking date (YYYY-MM-DD): ";
    cin >> date;
    bookRoom(roomID, name, date);
    break;
   }
   case 3: {
    cout << "Bookings:" << endl;
    for (const auto &booking : bookings) {
     cout << "Room " << booking.roomID << " booked by " << booking.name << " on " << booking.date << endl;
    }
    break;
   }
   case 4:
    saveBookings();
    return 0;
   default:
    cout << "Invalid choice." << endl;
  }
 }
}




