// follow on instagram - devish_h4x
// yt channel - celerio ff

#include <iostream>
#include <string>
#include <vector>
#include <fstream>

struct Student {
    std::string name;
    int age;
    std::string address;
    std::string phone;
    std::string motherName;
    std::string fatherName;
    float marks12th;
    std::string gender;
};

void saveToFile(const std::vector<Student>& students) {
    std::ofstream file("students.txt");
    for (const auto& s : students) {
        file << s.name << "," << s.age << "," << s.address << "," << s.phone << ","
             << s.motherName << "," << s.fatherName << "," << s.marks12th << "," << s.gender << "\n";
    }
    file.close();
}

void loadFromFile(std::vector<Student>& students) {
    std::ifstream file("students.txt");
    std::string line;
    while (std::getline(file, line)) {
        Student s;
        size_t pos = 0;
        pos = line.find(",");
        s.name = line.substr(0, pos);
        line = line.substr(pos + 1);
        pos = line.find(",");
        s.age = std::stoi(line.substr(0, pos));
        line = line.substr(pos + 1);
        pos = line.find(",");
        s.address = line.substr(0, pos);
        line = line.substr(pos + 1);
        pos = line.find(",");
        s.phone = line.substr(0, pos);
        line = line.substr(pos + 1);
        pos = line.find(",");
        s.motherName = line.substr(0, pos);
        line = line.substr(pos + 1);
        pos = line.find(",");
        s.fatherName = line.substr(0, pos);
        line = line.substr(pos + 1);
        pos = line.find(",");
        s.marks12th = std::stof(line.substr(0, pos));
        line = line.substr(pos + 1);
        s.gender = line;
        students.push_back(s);
    }
    file.close();
}

int main() {
    std::vector<Student> students;
    loadFromFile(students);

    while (true) {
        std::cout << "=== Student Details Manager ===\n";
        std::cout << "1. Add Student\n";
        std::cout << "2. View Students\n";
        std::cout << "3. Save and Exit\n";
        std::cout << "Choose an option: ";
        int choice;
        std::cin >> choice;
        std::cin.ignore(); // Ignore newline

        if (choice == 1) {
            Student s;
            std::cout << "Enter Name: ";
            std::getline(std::cin, s.name);
            std::cout << "Enter Age: ";
            std::cin >> s.age;
            std::cin.ignore();
            std::cout << "Enter Address: ";
            std::getline(std::cin, s.address);
            std::cout << "Enter Phone: ";
            std::getline(std::cin, s.phone);
            std::cout << "Enter Mother Name: ";
            std::getline(std::cin, s.motherName);
            std::cout << "Enter Father Name: ";
            std::getline(std::cin, s.fatherName);
            std::cout << "Enter 12th Marks: ";
            std::cin >> s.marks12th;
            std::cin.ignore();
            std::cout << "Enter Gender: ";
            std::getline(std::cin, s.gender);
            students.push_back(s);
            std::cout << "Student added!\n";
        } else if (choice == 2) {
            for (size_t i = 0; i < students.size(); ++i) {
                std::cout << "Student " << i + 1 << ":\n";
                std::cout << "Name: " << students[i].name << "\n";
                std::cout << "Age: " << students[i].age << "\n";
                std::cout << "Address: " << students[i].address << "\n";
                std::cout << "Phone: " << students[i].phone << "\n";
                std::cout << "Mother Name: " << students[i].motherName << "\n";
                std::cout << "Father Name: " << students[i].fatherName << "\n";
                std::cout << "12th Marks: " << students[i].marks12th << "\n";
                std::cout << "Gender: " << students[i].gender << "\n\n";
            }
        } else if (choice == 3) {
            saveToFile(students);
            std::cout << "Data saved. Exiting...\n";
            break;
        } else {
            std::cout << "Invalid choice.\n";
        }
    }

    return 0;
}
