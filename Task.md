***** MONGODB QUERIES *****

1. Find all the information about each products

         db.products.find()

![All Products](<Assets/Find all (1).JPG>)

2. Find the product price which are between 400 to 800

         db.products.find({product_price:{$gte:400,$lte:800}})

![Between 400to800](<Assets/Between 400 to 800.JPG>)

3. Find the product price which are not between 400 to 600


         db.products.find({product_price:{$not:{$gte:400,$lte:600}}})

![Not Between 400to600](<Assets/Not Between 400to600.JPG>)

4. List the four product which are grater than 500 in price

         db.products.find({product_price:{$gt:500}}).limit(4)

![Greater 500 and limit 4](<Assets/price greater 500 and limit 4.JPG>)

5. Find the product name and product material of each products

         db.products.find().projection({product_name:1,product_material:1,_id:0})

![name and material](<Assets/Product Name and Material.JPG>)

6. Find the product with a row id of 10

         db.products.find({id:"10"})

![id=10](<Assets/id = 10.JPG>)

7. Find only the product name and product material

         db.products.find().projection({product_name:1,product_material:1,_id:0})

![name and material](<Assets/Product Name and Material.JPG>)

8. Find all products which contain the value of soft in product material 

          db.products.find({product_material:'Soft'})

![Soft material](<Assets/Soft material.JPG>)

9. Find products which contain product color indigo  and product price 492.00

         db.products.find({$or:[{product_color:'indigo'},{product_price:492}]})

![indigo and 492](<Assets/indigo and 492.JPG>)

10. Delete the products which product price value are same

         db.products.aggregate([
           { $group: { _id: "$product_price", count: { $sum: 1 } } },
           { $match: { count: { $gt: 1 } } },
        ])
        .forEach((doc) => {
           db.products.deleteMany({ product_price: doc._id });
        });