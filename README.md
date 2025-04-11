# Full-Stack CRUD API

A full-stack web application that provides a dynamic and responsive user interface for managing data through Create, Read, Update, and Delete (CRUD) operations. The application utilizes React for the frontend, Flask for the backend, and SQLite for data storage. Chakra UI is employed to create a visually appealing and user-friendly interface.

---

## Features

- **Create**: Add new records to the database.
- **Read**: View existing records in a structured format.
- **Update**: Modify details of existing records.
- **Delete**: Remove records from the database.
- **Responsive Design**: Ensures usability across various devices and screen sizes.

---

## Technologies Used

- **Frontend**:
  - React
  - Chakra UI
  - Axios

- **Backend**:
  - Flask
  - Flask-CORS
  - SQLAlchemy
  - SQLite

---

## Project Structure

```
Full-Stack-CRUD-API/
├── backend/
│   ├── app.py
│   ├── models.py
│   ├── routes.py
│   └── database.db
├── frontend/
│   ├── public/
│   └── src/
│       ├── components/
│       ├── App.js
│       └── index.js
├── README.md
└── requirements.txt
```

---

## Setup Instructions

### Prerequisites

- Node.js and npm installed
- Python 3 installed
- Git installed

### Backend Setup

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   ```

3. Activate the virtual environment:
   - On macOS/Linux:
     ```bash
     source venv/bin/activate
     ```
   - On Windows:
     ```bash
     venv\Scripts\activate
     ```

4. Install the required packages:
   ```bash
   pip install -r requirements.txt
   ```

5. Run the Flask application:
   ```bash
   python app.py
   ```
   The backend server will start on `http://localhost:5000`.

### Frontend Setup

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```

2. Install the required packages:
   ```bash
   npm install
   ```

3. Start the React application:
   ```bash
   npm start
   ```
   The frontend will be accessible at `http://localhost:3000`.

---

## Usage

1. **Access the application**:
   Open your browser and navigate to `http://localhost:3000`.

2. **Perform CRUD operations**:
   - **Create**: Use the form to add new records.
   - **Read**: View the list of existing records.
   - **Update**: Click on the edit button next to a record to modify its details.
   - **Delete**: Click on the delete button to remove a record.

---

## API Endpoints

- `GET /api/items`: Retrieve all items.
- `GET /api/items/<id>`: Retrieve a specific item by ID.
- `POST /api/items`: Create a new item.
- `PUT /api/items/<id>`: Update an existing item by ID.
- `DELETE /api/items/<id>`: Delete an item by ID.

---

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch:
   ```bash
   git checkout -b feature/YourFeature
   ```
3. Commit your changes:
   ```bash
   git commit -m 'Add some feature'
   ```
4. Push to the branch:
   ```bash
   git push origin feature/YourFeature
   ```
5. Open a pull request.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.

