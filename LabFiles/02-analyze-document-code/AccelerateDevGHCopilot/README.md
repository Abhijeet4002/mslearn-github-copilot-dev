"""
To generate this README.md   this prompt is used
 #codebase I need you to generate the contents of a README.md file that I can use for the current code repository. Use "Library App" as the project title. The README file should include the following sections: Description, Project Structure, Key Classes and Interfaces, Usage, License. Format all sections as raw markdown. Use a bullet list with indents to represent the project structure. Do not include ".gitignore" or the ".github", "bin", and "obj" folders. I want add the suggested content to the README.md file that's open in the editor.
"""

# Library App

## Description

Library App is a modern .NET 9.0 console application that demonstrates clean architecture principles and dependency injection patterns. It provides a comprehensive library management system that allows users to search for patrons, view their loaned books, and manage library operations including membership renewals, loan extensions, and book returns. The application uses JSON files for data persistence and showcases best practices in C# application design.

## Project Structure

```
AccelerateDevGHCopilot/
├── src/
│   ├── Library.Console/
│   │   ├── Program.cs
│   │   ├── ConsoleApp.cs
│   │   ├── ConsoleState.cs
│   │   ├── CommonActions.cs
│   │   ├── appSettings.json
│   │   ├── Json/
│   │   │   ├── Authors.json
│   │   │   ├── Books.json
│   │   │   ├── BookItems.json
│   │   │   ├── Patrons.json
│   │   │   └── Loans.json
│   │   └── Library.Console.csproj
│   │
│   ├── Library.ApplicationCore/
│   │   ├── Entities/
│   │   │   ├── Author.cs
│   │   │   ├── Book.cs
│   │   │   ├── BookItem.cs
│   │   │   ├── Loan.cs
│   │   │   └── Patron.cs
│   │   ├── Interfaces/
│   │   │   ├── IPatronRepository.cs
│   │   │   ├── ILoanRepository.cs
│   │   │   ├── ILoanService.cs
│   │   │   └── IPatronService.cs
│   │   ├── Enums/
│   │   │   ├── ConsoleState.cs
│   │   │   └── CommonActions.cs
│   │   ├── Services/
│   │   │   ├── LoanService.cs
│   │   │   └── PatronService.cs
│   │   └── Library.ApplicationCore.csproj
│   │
│   └── Library.Infrastructure/
│       ├── Data/
│       │   ├── JsonData.cs
│       │   ├── JsonPatronRepository.cs
│       │   ├── JsonLoanRepository.cs
│       │   └── Library.Infrastructure.csproj
│       └── Library.Infrastructure.csproj
│
└── tests/
    └── [Test projects]
```

## Key Classes and Interfaces

### Core Entities
- **Patron**: Represents a library patron with membership information
- **Loan**: Tracks book loans with loan date, due date, and return date
- **Book**: Contains book information including title, author, and ISBN
- **BookItem**: Physical copy of a book with acquisition date and condition
- **Author**: Author information linked to books

### Repositories (Data Access Layer)
- **IPatronRepository**: Interface for patron data operations
  - `SearchPatrons(searchInput)`: Find patrons by name
  - `GetPatron(id)`: Retrieve patron details with loans
  - `UpdatePatron(patron)`: Update patron membership information
  
- **ILoanRepository**: Interface for loan data operations
  - `GetLoan(id)`: Retrieve loan details
  - `UpdateLoan(loan)`: Update loan dates

### Services (Business Logic Layer)
- **ILoanService**: Manages loan operations (extend loans, return books)
- **IPatronService**: Manages patron operations (renew memberships)

### Core Classes
- **ConsoleApp**: Main application class managing the state machine and user interactions
- **ConsoleState**: Enum representing application screens (PatronSearch, PatronSearchResults, PatronDetails, LoanDetails)
- **CommonActions**: Flags enum for user actions (Select, Quit, SearchPatrons, RenewPatronMembership, ExtendLoanedBook, ReturnLoanedBook)
- **JsonData**: Data manager handling JSON file I/O and entity population
  - `LoadData()`: Load all entities from JSON files
  - `SavePatrons(patrons)`: Save patron data to JSON
  - `SaveLoans(loans)`: Save loan data to JSON
  - `GetPopulatedPatron(patron)`: Enrich patron with related loans

## Usage

### Prerequisites
- .NET 9.0 SDK or later
- Visual Studio Code or Visual Studio 2022+

### Running the Application

1. **Navigate to the project directory**:
   ```bash
   cd src/Library.Console
   ```

2. **Run the application**:
   ```bash
   dotnet run
   ```

3. **Interact with the console menu**:
   - Enter a patron name to search
   - Select a patron from results using the number displayed
   - Use menu options:
     - `s` - Search for patrons
     - `m` - Renew patron membership
     - `e` - Extend a loaned book
     - `r` - Return a loaned book
     - `q` - Quit

### Application Flow

The application uses a state machine pattern:
1. **PatronSearch**: User enters a patron name
2. **PatronSearchResults**: Display matching patrons (max 20)
3. **PatronDetails**: Show selected patron's information and loaned books
4. **LoanDetails**: Manage specific loan operations

### Configuration

Edit `appSettings.json` to configure JSON file paths:
```json
{
  "JsonPaths": {
    "Authors": "Json/Authors.json",
    "Books": "Json/Books.json",
    "BookItems": "Json/BookItems.json",
    "Patrons": "Json/Patrons.json",
    "Loans": "Json/Loans.json"
  }
}
```

## License

This project is licensed under the MIT License. See the LICENSE file for details.
