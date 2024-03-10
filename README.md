From the provided diagram, we can see that the "Product" entity has a foreign key category_id that references the id of the "Product_Category" entity. This indicates a one-to-many relationship where one product category can have multiple products associated with it.
To ensure that each product in the "Product" table has a valid category assigned to it, you could implement a constraint on the category_id column of the "Product" table. This could be a foreign key constraint referencing the "Product_Category" table's id column, which would ensure that only valid category IDs can be assigned to products. Additionally, you could enforce this constraint at the application level by requiring that a valid category is selected when creating or updating a product.
CREATE TABLE product_category (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    product_inventory TEXT,
    created_at TIMESTAMP NOT NULL,
    modified_at TIMESTAMP NOT NULL
);

CREATE TABLE discount (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    desc TEXT,
    discount_percent DECIMAL NOT NULL,
    active BOOLEAN NOT NULL,
    created_at TIMESTAMP NOT NULL
);

CREATE TABLE product (
    id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    price DECIMAL NOT NULL,
    category_id INT NOT NULL,
    discount_id INT,
    deleted_at TIMESTAMP,
    CONSTRAINT fk_product_category
        FOREIGN KEY (category_id)
        REFERENCES product_category(id),
    CONSTRAINT fk_product_discount
        FOREIGN KEY (discount_id)
        REFERENCES discount(id)
);
