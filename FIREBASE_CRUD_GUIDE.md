# Firebase CRUD Guide for Beginners

This guide explains how to Create, Read, Update, and Delete (CRUD) data in your Firebase Firestore database using the existing setup.

---

## 1. Understanding Firestore

Firestore is a NoSQL database. It stores data in **Documents**, which are organized into **Collections**.
- **Collection**: Like a folder (e.g., `users`, `moods`).
- **Document**: Like a file inside the folder (e.g., `user_123`).
- **Data**: Key-value pairs inside the document (e.g., `name: "Raghav"`).

## 2. Accessing the Database in Code

In our project, we use the `firebase-admin` SDK in Python (`backend/database.py`) and the `firebase` SDK in JavaScript (`frontend/src/services/firestore.js`).

### Python (Backend)

First, ensure `db` is initialized:
```python
from firebase_admin import firestore
db = firestore.client()
```

#### Create (Add Data)
```python
# Add a new document with a specific ID
db.collection("users").document("user_123").set({
    "name": "Raghav",
    "email": "raghav@example.com"
})

# Add a new document with an auto-generated ID
db.collection("users").document("user_123").collection("moods").add({
    "emoji": "😊",
    "score": 5
})
```

#### Read (Get Data)
```python
# Get a single document
doc = db.collection("users").document("user_123").get()
if doc.exists:
    print(doc.to_dict())

# Get multiple documents (Query)
docs = db.collection("users").where("email", "==", "raghav@example.com").stream()
for doc in docs:
    print(doc.id, doc.to_dict())
```

#### Update (Modify Data)
```python
# Update specific fields (doesn't overwrite the whole document)
db.collection("users").document("user_123").update({
    "bio": "Updated bio"
})
```

#### Delete (Remove Data)
```python
# Delete a document
db.collection("users").document("user_123").delete()
```

### JavaScript (Frontend)

First, import `db` from your config:
```javascript
import { db } from '../config';
import { doc, getDoc, setDoc, updateDoc, deleteDoc, collection, addDoc } from "firebase/firestore";
```

#### Create
```javascript
// Add with specific ID
await setDoc(doc(db, "users", "user_123"), {
  name: "Raghav",
  email: "raghav@example.com"
});

// Add with auto-ID
await addDoc(collection(db, "moods"), {
  emoji: "😊",
  score: 5
});
```

#### Read
```javascript
const docRef = doc(db, "users", "user_123");
const docSnap = await getDoc(docRef);

if (docSnap.exists()) {
  console.log("Document data:", docSnap.data());
} else {
  console.log("No such document!");
}
```

#### Update
```javascript
const userRef = doc(db, "users", "user_123");
await updateDoc(userRef, {
  bio: "New Bio"
});
```

#### Delete
```javascript
await deleteDoc(doc(db, "users", "user_123"));
```

## 3. Managing Data in Firebase Console

You can also manually manage data:
1.  Go to [console.firebase.google.com](https://console.firebase.google.com).
2.  Select your project.
3.  Click **Firestore Database** in the left menu.
4.  **Start Collection**: Click to create a new collection (e.g., `users`).
5.  **Add Document**: Click to add a document. You can generate an ID or type one.
6.  **Add Field**: Type field name (e.g., `name`) and value (e.g., `Raghav`).
7.  **Edit/Delete**: Click the pencil icon to edit or the menu (three dots) to delete.

## 4. Common Rules & Tips
- **Security Rules**: In production, set rules in the "Rules" tab to restrict who can read/write.
  ```
  allow read, write: if request.auth != null;
  ```
- **Cost**: Reads and writes cost money (free tier is generous). Don't fetch unnecessary data in loops.
- **Indexes**: If you do complex queries (e.g., `where` + `orderBy`), Firebase will ask you to create an index. Just click the link in the error message.
