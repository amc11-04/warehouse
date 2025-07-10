# warehouse
import os
import zipfile

# สร้างโครงสร้างโปรเจกต์ React อย่างง่าย
project_name = "warehouse-react-app"
os.makedirs(f"/mnt/data/{project_name}/src", exist_ok=True)

# ไฟล์ index.html (public)
index_html = """<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>ระบบคลังสินค้า</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
"""
with open(f"/mnt/data/{project_name}/public/index.html", "w") as f:
    os.makedirs(f"/mnt/data/{project_name}/public", exist_ok=True)
    f.write(index_html)

# ไฟล์ App.js
app_js = """import { useState, useEffect } from 'react';

export default function App() {
  const [products, setProducts] = useState([]);
  const [name, setName] = useState('');
  const [quantity, setQuantity] = useState('');

  useEffect(() => {
    const stored = localStorage.getItem('warehouse');
    if (stored) setProducts(JSON.parse(stored));
  }, []);

  useEffect(() => {
    localStorage.setItem('warehouse', JSON.stringify(products));
  }, [products]);

  const addProduct = () => {
    if (name && quantity) {
      const newProduct = {
        id: Date.now(),
        name,
        quantity: parseInt(quantity)
      };
      setProducts([...products, newProduct]);
      setName('');
      setQuantity('');
    }
  };

  const deleteProduct = (id) => {
    setProducts(products.filter(p => p.id !== id));
  };

  return (
    <div className="p-6 max-w-xl mx-auto">
      <h1 className="text-2xl font-bold mb-4">📦 ระบบคลังสินค้า (React App)</h1>

      <div className="mb-4 flex gap-2">
        <input
          type="text"
          placeholder="ชื่อสินค้า"
          value={name}
          onChange={(e) => setName(e.target.value)}
          className="border p-2 rounded w-1/2"
        />
        <input
          type="number"
          placeholder="จำนวน"
          value={quantity}
          onChange={(e) => setQuantity(e.target.value)}
          className="border p-2 rounded w-1/4"
        />
        <button
          onClick={addProduct}
          className="bg-blue-500 text-white px-4 py-2 rounded"
        >
          เพิ่มสินค้า
        </button>
      </div>

      <table className="w-full border">
        <thead>
          <tr className="bg-gray-200">
            <th className="border px-2 py-1">ชื่อสินค้า</th>
            <th className="border px-2 py-1">จำนวน</th>
            <th className="border px-2 py-1">ลบ</th>
          </tr>
        </thead>
        <tbody>
          {products.map(product => (
            <tr key={product.id}>
              <td className="border px-2 py-1">{product.name}</td>
              <td className="border px-2 py-1">{product.quantity}</td>
              <td className="border px-2 py-1 text-center">
                <button
                  className="bg-red-500 text-white px-2 py-1 rounded"
                  onClick={() => deleteProduct(product.id)}
                >ลบ</button>
              </td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}
"""
with open(f"/mnt/data/{project_name}/src/App.js", "w") as f:
    f.write(app_js)

# ไฟล์ index.js
index_js = """import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
"""
with open(f"/mnt/data/{project_name}/src/index.js", "w") as f:
    f.write(index_js)

# ไฟล์ index.css
index_css = """body {
  font-family: sans-serif;
  padding: 0;
  margin: 0;
}
"""
with open(f"/mnt/data/{project_name}/src/index.css", "w") as f:
    f.write(index_css)

# สร้าง package.json อย่างง่าย
package_json = """{
  "name": "warehouse-app",
  "version": "1.0.0",
  "private": true,
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build"
  }
}
"""
with open(f"/mnt/data/{project_name}/package.json", "w") as f:
    f.write(package_json)
