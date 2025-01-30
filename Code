import { useState, useEffect } from "react";
import axios from "axios";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { Card, CardContent } from "@/components/ui/card";
import { fetchUsers, addUser, updateUser, deleteUser } from "@/services/api";

export default function UserManagement() {
  const [users, setUsers] = useState([]);
  const [newUser, setNewUser] = useState({ firstName: "", lastName: "", email: "", department: "" });
  const [editingUser, setEditingUser] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetchUsers()
      .then((data) => setUsers(data))
      .catch(() => setError("Failed to fetch users"));
  }, []);

  const handleAddUser = () => {
    addUser(newUser)
      .then((data) => setUsers([...users, data]))
      .catch(() => setError("Failed to add user"));
  };

  const handleEditUser = (id) => {
    updateUser(id, editingUser)
      .then(() => {
        setUsers(users.map(user => (user.id === id ? editingUser : user)));
        setEditingUser(null);
      })
      .catch(() => setError("Failed to update user"));
  };

  const handleDeleteUser = (id) => {
    deleteUser(id)
      .then(() => setUsers(users.filter(user => user.id !== id)))
      .catch(() => setError("Failed to delete user"));
  };

  return (
    <div className="p-4">
      <h1 className="text-xl font-bold mb-4">User Management Dashboard</h1>
      {error && <p className="text-red-500">{error}</p>}
      <Card>
        <CardContent className="p-4">
          <h2 className="text-lg font-semibold">Add User</h2>
          <Input placeholder="First Name" onChange={(e) => setNewUser({ ...newUser, firstName: e.target.value })} />
          <Input placeholder="Last Name" onChange={(e) => setNewUser({ ...newUser, lastName: e.target.value })} />
          <Input placeholder="Email" type="email" onChange={(e) => setNewUser({ ...newUser, email: e.target.value })} />
          <Input placeholder="Department" onChange={(e) => setNewUser({ ...newUser, department: e.target.value })} />
          <Button onClick={handleAddUser} className="mt-2">Add User</Button>
        </CardContent>
      </Card>
      <div className="mt-4">
        <h2 className="text-lg font-semibold">User List</h2>
        {users.map((user) => (
          <Card key={user.id} className="mt-2">
            <CardContent className="p-4">
              <p>{user.firstName} {user.lastName} ({user.email}) - {user.department}</p>
              <Button onClick={() => setEditingUser(user)}>Edit</Button>
              <Button onClick={() => handleDeleteUser(user.id)} className="ml-2 bg-red-500">Delete</Button>
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}
