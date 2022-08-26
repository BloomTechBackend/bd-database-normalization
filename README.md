### Data Normalization

In this exercise we walk through the process of normalizing a collection of data into a relational database model.
Below we have the Original Data of Customers and their Orders.

*These orders have been placed by Captain and Duchess the Tuxedo and Calico cats, as well as Lexi the Great Pyrenees dog.*

<details open><summary>Original Data</summary>
<p>

Data Table

| Customer Name | Customer Location | C Location 2   | Order Number | Order Total | Product   | Product Unit Price | Quantity Ordered |
|---------------|-------------------|----------------|--------------|-------------|-----------|--------------------|------------------|
| Captain       | Cat Tree          | Living Room    | AAA          | 99.99       | Crunchies | 1.00               | 5                |
| Captain       | Cat Tree          | Living Room    | AAA          | 99.99       | Tuna      | 2.00               | 3                |
| Captain       | **Box Fort**      | Living Room    | AAA          | 99.99       | Bedding   | 3.00               | 7                |
| Duchess       | Box Fort          | Kid's Room     | BBB          | 99.99       | Crunchies | 1.00               | 2                |
| Duchess       | Box Fort          | Kid's Room     | BBB          | 99.99       | Tuna      | 2.00               | 1                |
| Duchess       | Box Fort          | Kid's Room     | BBB          | 99.99       | Collar    | 5.00               | 3                |
| Duchess       | Box Fort          | Kid's Room     | BBB          | 99.99       | Collar    | 5.00               | 5                |
| Duchess       | Box Fort          | Kid's Room     | BBB          | 99.99       | Cat Toy   | 4.00               | 4                |
| Captain       | Cat Tree          | Living Room    | CCC          | 99.99       | Cat Toy   | 4.00               | 8                |
| Captain       | Cat Tree          | Living Room    | CCC          | 99.99       | Tuna      | 2.00               | 1                |
| Lexi          | Office Futon      |                |              |             |           |                    |                  |

</p>
</details>

<details><summary>1NF - Separate Data into related fields, No repeated fields</summary>
<p>

Customer Table

| Customer Id | Name     |
|-------------|----------|
| 1           | Captain  |
| 2           | Duchess  |
| 3           | Lexi     |

Order Table

| Order Entry Id | Customer Id   | Order Number | Order Total | Product   | Product Unit Price | Quantity Ordered |
|----------------|---------------|--------------|-------------|-----------|--------------------|------------------|
| 1              | 1             | AAA          | 99.99       | Crunchies | 1.00               | 5                |
| 2              | 1             | AAA          | 99.99       | Tuna      | 2.00               | 3                |
| 3              | 1             | AAA          | 99.99       | Bedding   | 3.00               | 7                |
| 4              | 2             | BBB          | 99.99       | Crunchies | 1.00               | 2                |
| 5              | 2             | BBB          | 99.99       | Tuna      | 2.00               | 1                |
| 6              | 2             | BBB          | 99.99       | Collar    | 5.00               | 3                |
| 7              | 2             | BBB          | 99.99       | Collar    | 5.00               | 5                |
| 8              | 2             | BBB          | 99.99       | Cat Toy   | 4.00               | 4                |
| 9              | 1             | CCC          | 99.99       | Cat Toy   | 4.00               | 8                |
| 10             | 1             | CCC          | 99.99       | Tuna      | 2.00               | 1                |

Location Table

| Location Id | Customer | Location       |
|-------------|----------|----------------|
| 1           | 1        | Cat Tree       |
| 2           | 1        | Living Room    |
| 3           | 2        | Box Fort       |
| 4           | 2        | Kid's Room     |
| 5           | 3        | Office Futon   |

</p>
</details>

<details><summary>2NF - Multiple Records Data Not Repeated</summary>
<p>

Customer Table

| Customer Id | Name     |
|-------------|----------|
| 1           | Captain  |
| 2           | Duchess  |
| 3           | Lexi     |

Product Table

| Product Id | Product   | Product Unit Price |
|------------|-----------|--------------------|
| 1          | Crunchies | 1.00               |
| 2          | Tuna      | 2.00               |
| 3          | Bedding   | 3.00               |
| 4          | Collar    | 5.00               |
| 5          | Cat Toy   | 4.00               |

Order Table

| Order Id | Customer Id   | Order Number | Order Total |
|----------|---------------|--------------|-------------|
| 1        | 1             | AAA          | 99.99       |
| 2        | 2             | BBB          | 99.99       |
| 3        | 1             | CCC          | 99.99       |

Order Product Table

| Order Product Id | Order Id | Product Id | Quantity Ordered |
|------------------|----------|------------|------------------|
| 1                | 1        | 1          | 5                |
| 2                | 1        | 2          | 3                |
| 3                | 1        | 3          | 7                |
| 4                | 2        | 1          | 2                |
| 5                | 2        | 2          | 1                |
| 6                | 2        | 4          | 3                |
| 7                | 2        | 4          | 5                |
| 8                | 2        | 5          | 4                |
| 9                | 3        | 5          | 8                |
| 10               | 3        | 2          | 1                |

Location Table

| Location Id | Customer | Location       |
|-------------|----------|----------------|
| 1           | 1        | Cat Tree       |
| 2           | 1        | Living Room    |
| 3           | 2        | Box Fort       |
| 4           | 2        | Kid's Room     |
| 5           | 3        | Cat Tree       |

</p>
</details>

<details><summary>3NF - Duplicated Data Removed, No Derived Data</summary>
<p>

Customer Table

| Customer Id | Name     |
|-------------|----------|
| 1           | Captain  |
| 2           | Duchess  |
| 3           | Lexi     |

Product Table

| Product Id | Product   | Product Unit Price |
|------------|-----------|--------------------|
| 1          | Crunchies | 1.00               |
| 2          | Tuna      | 2.00               |
| 3          | Bedding   | 3.00               |
| 4          | Collar    | 5.00               |
| 5          | Cat Toy   | 4.00               |

Order Table

| Order Id | Customer Id   | Order Number |
|----------|---------------|--------------|
| 1        | 1             | AAA          |
| 2        | 2             | BBB          |
| 3        | 1             | CCC          |

Order Product Table

| Order Product Id | Order Id | Product Id | Quantity Ordered |
|------------------|----------|------------|------------------|
| 1                | 1        | 1          | 5                |
| 2                | 1        | 2          | 3                |
| 3                | 1        | 3          | 7                |
| 4                | 2        | 1          | 2                |
| 5                | 2        | 2          | 1                |
| 6                | 2        | 4          | 8                |
| 7                | 2        | 5          | 4                |
| 8                | 3        | 5          | 8                |
| 9                | 3        | 2          | 1                |

Notice that in order 2, COLLAR was ordered twice. These items orders are combined here

Location Table

| Location Id | Customer | Location       |
|-------------|----------|----------------|
| 1           | 1        | Cat Tree       |
| 2           | 1        | Living Room    |
| 3           | 2        | Box Fort       |
| 4           | 2        | Kid's Room     |
| 5           | 3        | Cat Tree       |

</p>
</details>
