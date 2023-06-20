#include <iostream>
#include <fstream>
#include <string>
#include <vector>

class Contact {
public:
	Contact(const std::string& name, const std::string& surname, const std::string& phoneNumber, const std::string& email, const std::string& address) {
		this->name = name;
		this->surname = surname; 
		this->phoneNumber = phoneNumber;
		this->email = email;
		this->address = address;
	}
		

	void setPhoneNumber(const std::string& newPhoneNumber) { this->phoneNumber = newPhoneNumber; }
	void setEmail(const std::string& newEmail) { this->email = newEmail; }
	void setAddress(const std::string& newAddress) { this->address = newAddress; }

	std::string getName() const { return name; }
	std::string getSurname() const { return surname; }
	std::string getPhoneNumber() const { return phoneNumber; }
	std::string getEmail() const { return email; }
	std::string getAddress() const { return address; }

	void displayInfo() const {
		std::cout << "Name: " << name << std::endl;
		std::cout << "Surname: " << surname << std::endl;
		std::cout << "Phone Number: " << phoneNumber << std::endl;
		std::cout << "Email: " << email << std::endl;
		std::cout << "Address: " << address << std::endl;
		std::cout << "------------------------" << std::endl;
	}

private:
	std::string name;
	std::string surname;
	std::string phoneNumber;
	std::string email;
	std::string address;
};

class AddressBook {
public:
	void addContact(const Contact& contact) {
		contacts.push_back(contact);
	}

	void removeContact(const std::string& name, const std::string& surname) {
		for (auto it = contacts.begin(); it != contacts.end(); ++it) {
			if (it->getName() == name && it->getSurname() == surname) {
				contacts.erase(it);
				break;
			}
		}
	}

	void updateContact(const std::string& name, const std::string& surname) {
		for (auto& contact : contacts) {
			if (contact.getName() == name && contact.getSurname() == surname) {

				std::cout << "Enter the new phone number: ";
				std::string newPhoneNumber;
				std::cin >> newPhoneNumber;
				contact.setPhoneNumber(newPhoneNumber);

				std::cout << "Enter the new email: ";
				std::string newEmail;
				std::cin >> newEmail;
				contact.setEmail(newEmail);

				std::cout << "Enter the new address: ";
				std::cin.ignore(); 
				std::string newAddress;
				std::getline(std::cin, newAddress);
				contact.setAddress(newAddress);
				break;
			}
		}
	}


	void searchContacts(const std::string& searchStr) const {
		bool found = false;
		for (const auto& contact : contacts) {
			if (contact.getName().find(searchStr) != std::string::npos ||
				contact.getSurname().find(searchStr) != std::string::npos ||
				contact.getPhoneNumber().find(searchStr) != std::string::npos ||
				contact.getEmail().find(searchStr) != std::string::npos ||
				contact.getAddress().find(searchStr) != std::string::npos) {
				contact.displayInfo();
				found = true;
			}
		}

		if (!found) {
			std::cout << "No contacts found with the given search criteria." << std::endl;
		}
	}

	void displayAllContacts() const {
		if (contacts.empty()) {
			std::cout << "No contacts available." << std::endl;
			return;
		}

		for (const auto& contact : contacts) {
			contact.displayInfo();
		}
	}

	void saveContactsToFile(const std::string& filename) const {
		std::ofstream outFile(filename);

		if (outFile.is_open()) {
			for (const auto& contact : contacts) {
				outFile << contact.getName() << ","
					<< contact.getSurname() << ","
					<< contact.getPhoneNumber() << ","
					<< contact.getEmail() << ","
					<< contact.getAddress() << std::endl;
			}

			outFile.close();
			std::cout << "Contacts saved to file: " << filename << std::endl;
		}
		else {
			std::cerr << "Unable to save contacts to file." << std::endl;
		}
	}

	void loadContactsFromFile(const std::string& filename) {
		std::ifstream inFile(filename);

		if (inFile.is_open()) {
			contacts.clear(); 

			std::string line;
			while (std::getline(inFile, line)) {
				std::string name, surname, phoneNumber, email, address;

				size_t pos1 = line.find(',');
				if (pos1 != std::string::npos) {
					name = line.substr(0, pos1);

					size_t pos2 = line.find(',', pos1 + 1);
					if (pos2 != std::string::npos) {
						surname = line.substr(pos1 + 1, pos2 - pos1 - 1);

						size_t pos3 = line.find(',', pos2 + 1);
						if (pos3 != std::string::npos) {
							phoneNumber = line.substr(pos2 + 1, pos3 - pos2 - 1);

							size_t pos4 = line.find(',', pos3 + 1);
							if (pos4 != std::string::npos) {
								email = line.substr(pos3 + 1, pos4 - pos3 - 1);
								address = line.substr(pos4 + 1);
							}
						}
					}
				}

				Contact contact(name, surname, phoneNumber, email, address);
				contacts.push_back(contact);
			}

			inFile.close();
			std::cout << "Contacts loaded from file: " << filename << std::endl;
		}
		else {
			std::cerr << "Unable to load contacts from file." << std::endl;
		}
	}

private:
	std::vector<Contact> contacts;
};


bool isValidEmail(const std::string& email) {
	return email.find('@') != std::string::npos && email.find('.') != std::string::npos;
}

bool isValidPhoneNumber(const std::string& phoneNumber) {
	return phoneNumber.find_first_not_of("0123456789") == std::string::npos;
}

int main() {
	AddressBook addressBook;
	std::string filename = "contacts.txt";

	addressBook.loadContactsFromFile(filename);

	while (true) {
		std::cout << "------------------------" << std::endl;
		std::cout << "Address Book Menu:" << std::endl;
		std::cout << "1. Add Contact" << std::endl;
		std::cout << "2. Remove Contact" << std::endl;
		std::cout << "3. Update Contact" << std::endl;
		std::cout << "4. Search Contacts" << std::endl;
		std::cout << "5. Display All Contacts" << std::endl;
		std::cout << "6. Save Contacts to File" << std::endl;
		std::cout << "7. Exit" << std::endl;
		std::cout << "------------------------" << std::endl;
		std::cout << "Enter your choice: ";

		int choice;
		std::cin >> choice;

		
		switch (choice) {
		case 1: {
			std::cout << "Enter name: ";
			std::string name;
			std::cin >> name;

			std::cout << "Enter surname: ";
			std::string surname;
			std::cin >> surname;

			std::cout << "Enter phone number: ";
			std::string phoneNumber;
			std::cin >> phoneNumber;
			while (!isValidPhoneNumber(phoneNumber)) {
				std::cout << "Invalid phone number. Please enter a valid phone number: ";
				std::cin >> phoneNumber;
			}

			std::cout << "Enter email: ";
			std::string email;
			std::cin >> email;
			while (!isValidEmail(email)) {
				std::cout << "Invalid email address. Please enter a valid email: ";
				std::cin >> email;
			}

			std::cout << "Enter address: ";
			std::cin.ignore(); 
			std::string address;
			std::getline(std::cin, address);

			Contact contact(name, surname, phoneNumber, email, address);
			addressBook.addContact(contact);
			std::cout << "Contact added successfully." << std::endl;
			break;
		}
		case 2: {
			std::cout << "Enter name: ";
			std::string name;
			std::cin >> name;

			std::cout << "Enter surname: ";
			std::string surname;
			std::cin >> surname;

			addressBook.removeContact(name, surname);
			std::cout << "Contact removed successfully." << std::endl;
			break;
		}
		case 3: {
			std::cout << "Enter name: ";
			std::string name;
			std::cin >> name;

			std::cout << "Enter surname: ";
			std::string surname;
			std::cin >> surname;

			addressBook.updateContact(name, surname);
			std::cout << "Contact updated successfully." << std::endl;
			break;
		}
		case 4: {
			std::cout << "Enter search string: ";
			std::string searchStr;
			std::cin >> searchStr;
			addressBook.searchContacts(searchStr);
			break;
		}
		case 5:
			addressBook.displayAllContacts();
			break;
		case 6:
			addressBook.saveContactsToFile(filename);
			break;
		case 7:
			addressBook.saveContactsToFile(filename);
			std::cout << "Exiting the program." << std::endl;
			return 0;
		default:
			std::cout << "Invalid choice. Please try again." << std::endl;
		}
	}
}
