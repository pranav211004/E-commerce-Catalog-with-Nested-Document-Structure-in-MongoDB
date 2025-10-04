/*
🛒 E-Commerce Catalog with Nested Document Structure
📘 Overview: This script demonstrates how to build an E-Commerce catalog in MongoDB with nested documents. Each product includes name, price, category, and variants (color, size, stock).

⚙️ Features:

Insert sample products with multiple variants
Retrieve all products
Filter by category
Project specific nested fields
Update nested variant stock
========================================================= 🧩 Collection Structure
{ name: "string", price: "number", category: "string", variants: [ { color: "string", size: "string", stock: "number" } ] }
*/

// 1️⃣ Create and Use Database use ecommerceDB;

// 2️⃣ Insert Sample Products db.products.insertMany([ { name: "RoadWare Car Seat Cover", price: 1999, category: "Accessories", variants: [ { color: "Black", size: "Standard", stock: 25 }, { color: "Beige", size: "Large", stock: 10 } ] }, { name: "RoadWare LED Headlight", price: 3499, category: "Lighting", variants: [ { color: "White", size: "Universal", stock: 50 }, { color: "Blue", size: "Universal", stock: 30 } ] }, { name: "RoadWare Car Floor Mat", price: 1299, category: "Interior", variants: [ { color: "Black", size: "Medium", stock: 15 }, { color: "Gray", size: "Large", stock: 8 } ] } ]);

// 3️⃣ Retrieve All Products print("\n=== All Products ==="); db.products.find().pretty();

// 4️⃣ Filter Products by Category (Example: Lighting) print("\n=== Lighting Category Products ==="); db.products.find({ category: "Lighting" }).pretty();

// 5️⃣ Project Specific Variant Details (color & stock only) print("\n=== Product Variant Details ==="); db.products.find( {}, { name: 1, "variants.color": 1, "variants.stock": 1, _id: 0 } ).pretty();

// 6️⃣ Find Products having Variant Color = Black print("\n=== Products with Black Variant ==="); db.products.find({ "variants.color": "Black" }).pretty();

// 7️⃣ Update Stock of Specific Variant print("\n=== Updating Stock for Blue LED Headlight ==="); db.products.updateOne( { name: "RoadWare LED Headlight", "variants.color": "Blue" }, { $inc: { "variants.$.stock": 5 } } );

// 8️⃣ Verify Update print("\n=== Updated LED Headlight Document ==="); db.products.find({ name: "RoadWare LED Headlight" }).pretty();

/*
📄 README SECTION
🛒 E-Commerce Catalog (MongoDB)
💾 How to Run:
Open MongoDB shell or VS Code MongoDB playground.
Save this file as ecommerce_catalog.js.
Execute: load("ecommerce_catalog.js")
🧠 Key Concepts:
Nested Documents: Arrays inside a single document.
Dot Notation: Access nested fields easily.
Positional Operator ($): Update specific nested items.
🧱 Example Queries:
👉 View All Products db.products.find().pretty();

👉 Filter by Category db.products.find({ category: "Lighting" }).pretty();

👉 Project Variant Details db.products.find({}, { name: 1, "variants.color": 1, "variants.stock": 1, _id: 0 });

👉 Find Specific Variant db.products.find({ "variants.color": "Black" }).pretty();

👉 Update Variant Stock db.products.updateOne( { name: "RoadWare LED Headlight", "variants.color": "Blue" }, { $inc: { "variants.$.stock": 5 } } );

*/
