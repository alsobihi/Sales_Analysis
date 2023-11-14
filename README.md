# Sales_Analysis
## تنظيف بيانات المبيعات 
مصدر البيانات: [https://www.kaggle.com/datasets/serdarsozturk/salesanalysis](https://www.kaggle.com/datasets/serdarsozturk/salesanalysis)

### الخطوة الأولى حصر الجداول
بعد تحميل البيانات لجميع الأشهر قم بأخذ نظرة سريعة على البيانات ومحاولة فهم سياق البيانات 
يجب علينا أن نتحقق من عدد العواميد وترتيبها
* Sales_April_2019
* Sales_August_2019
* Sales_December_2019
* Sales_February_2019
* Sales_January_2019
* Sales_July_2019
* Sales_June_2019
* Sales_March_2019
* Sales_May_2019
* Sales_November_2019
* Sales_October_2019
* Sales_September_2019



#### يجب توحيد ترتيب العواميد بالشكل التالي لجميع الجداول 
````
    - Order ID 
    - Product 
    - Quantity Ordered 
    - Price Each 
    - Order Date 
    - Purchase Address
````





#### دمج الجداول (جميع الأشهر)
دمج جميع الجداول بإستخدام union وحفظ البيانات بجدول جديد بأسم بـ `Sales_2019`

````
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_April_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_August_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_December_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_February_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_January_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_July_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_June_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_March_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_May_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_November_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_October_2019` 
UNION ALL
SELECT * FROM `hrkpi-1.Sales_Analysis.Sales_September_2019` 
````


#### إعادة تسمية العواميد 


قم بإعادة تسمية العواميد ليكون بالشكل التالي:


````
    - Order_ID 
    - Product 
    - Quantity 
    - Price_Each 
    - Order_Date 
    - Purchase_Address
````


````
SELECT
  string_field_0 AS Order_ID,
  string_field_1 AS Product,
  string_field_2 AS Quantity,
  string_field_3 AS Price_Each,
  string_field_4 AS Order_Date,
  string_field_5 AS Purchase_Address
FROM
  `hrkpi-1.Sales_Analysis.Sales_2019`

````

### الخطوة الثانية تنظيف البيانات

#### قم بحساب عدد الصفوف في الجدول

````
SELECT count(*) FROM `hrkpi-1.Sales_Analysis.Sales2019_part2` 
````

````
186862
````





#### قم بحساب عدد الصفوف الفارغة `NULL`

````
SELECT
  COUNT(*)
FROM
  `hrkpi-1.Sales_Analysis.Sales2019_part2`
WHERE
  Order_ID IS NULL
  AND Product IS NULL
  AND Quantity IS NULL
  AND Price_Each IS NULL
  AND Order_Date IS NULL
  AND Purchase_Address IS NULL
````

````
545
````



#### قم بحذف الصفوف الفارغة
بعد الحدذف تأكد من ان عدد الصفوف مطابق للصفوف الفارغة واجمالي عدد الصفوف الحالي 

````
DELETE
FROM
  `hrkpi-1.Sales_Analysis.Sales2019_part2`
WHERE
  Order_ID IS NULL
  AND Product IS NULL
  AND Quantity IS NULL
  AND Price_Each IS NULL
  AND Order_Date IS NULL
  AND Purchase_Address IS NULL
````

````
545 Rows Deleted
````




#### قم بحساب الصفوف المتكررة

````
SELECT COUNT(*)
FROM
  `hrkpi-1.Sales_Analysis.Sales2019_part2`
WHERE Order_ID = 'Order ID'
````
````
366
````





#### قم بحذف الصفوف المتكررة

````
DELETE
FROM
  `hrkpi-1.Sales_Analysis.Sales2019_part2`
WHERE Order_ID = 'Order ID'
````

````
367 Rows Deleted
````



### الخطوة الثالثة تحويل البيانات


#### أضف عامود جديد بأسم `Month` وضع أسم الشهر المناسب في كل صف

````

SELECT 
*,
EXTRACT (MONTH FROM date(PARSE_DATETIME('%m/%d/%y %H:%M', Order_Date)) ) AS Month
 



--- Order_Date
FROM `hrkpi-1.Sales_Analysis.Sales2019_part2`

````






#### أضف عامود جديد بأسم  `City` وضع فيه أسم مدينة العميل

````
SELECT 
* ,
REGEXP_EXTRACT(Purchase_Address, ',s*(.*?),') AS city_name

FROM `hrkpi-1.Sales_Analysis.Sales_2019_part2_withmonth` 
````


#### أضف عامود جديد بأسم  `Country` وضع فيه أسم الدولة USA

````
SELECT 
* ,
 CONCAT('USA') AS Country
FROM `hrkpi-1.Sales_Analysis.Sales_2019_part2_withmonth` 
````

#### أضرب عامود الكمية مع عامود سعر الحبة ليظهر الإجمالي

````
CAST(Quantity AS FLOAT64) * CAST(Price_Each AS FLOAT64) AS Total_Price
````


#### ترتيب البيانات النهائي

````
    - Order_ID 
    - Product 
    - Quantity 
    - Price_Each 
    - Order_Date 
    - Purchase_Address
    - Month
    - Country
    - City_Name
    - Total_Price

````


### معلومات عامة عن البيانات

#### عدد الصفوف في الجدول

````
SELECT COUNT(*) AS Total_Rows FROM `hrkpi-1.Sales_Analysis.Sales_2019_part3` 
````

````
185950
````

#### اجمالي المبيعات

````
SELECT
  SUM(Total_Price) AS Total_sales
FROM
  `hrkpi-1.Sales_Analysis.Sales_2019_part3`
````

````
34492035.969941095
````




### النتيجة


``
SELECT
  *
FROM
  `hrkpi-1.Sales_Analysis.Sales_2019_part3`
LIMIT
  25
``


| **Order_ID** | **Product** | **Quantity** | **Price_Each** | **Order_Date** | **Purchase_Address**                     | **Month** | **Country** | **city_name** | **Total_Price** |
|--------------|-------------|--------------|----------------|----------------|------------------------------------------|-----------|-------------|---------------|-----------------|
| 143869       | iPhone      | 1            | 700            | 01/11/19 16:17 | "481 Center St, San Francisco, CA 94016" | 1         | USA         | San Francisco | 700.0           |
| 148231       | iPhone      | 1            | 700            | 01/15/19 20:43 | "204 2nd St, Boston, MA 02215"           | 1         | USA         | Boston        | 700.0           |
| 145672       | iPhone      | 1            | 700            | 01/18/19 18:19 | "465 12th St, San Francisco, CA 94016"   | 1         | USA         | San Francisco | 700.0           |
| 145911       | iPhone      | 1            | 700            | 01/27/19 10:14 | "347 Maple St, Seattle, WA 98101"        | 1         | USA         | Seattle       | 700.0           |
| 149886       | iPhone      | 1            | 700            | 01/11/19 16:57 | "404 1st St, New York City, NY 10001"    | 1         | USA         | New York City | 700.0           |
| 143432       | iPhone      | 1            | 700            | 01/06/19 00:44 | "794 South St, New York City, NY 10001"  | 1         | USA         | New York City | 700.0           |
| 142010       | iPhone      | 1            | 700            | 01/04/19 06:28 | "511 2nd St, Portland, OR 97035"         | 1         | USA         | Portland      | 700.0           |
| 141437       | iPhone      | 1            | 700            | 01/10/19 15:40 | "377 Meadow St, New York City, NY 10001" | 1         | USA         | New York City | 700.0           |
| 141888       | iPhone      | 1            | 700            | 01/09/19 11:01 | "17 Spruce St, Los Angeles, CA 90001"    | 1         | USA         | Los Angeles   | 700.0           |
| 143694       | iPhone      | 1            | 700            | 01/03/19 19:20 | "265 6th St, New York City, NY 10001"    | 1         | USA         | New York City | 700.0           |





> **Note**
> لمشاهدة النتيجة النهائية قم بالزيارة هنا
> * LookerStudio  [Sales Report Page](https://lookerstudio.google.com/embed/reporting/8df40b83-ed36-4355-a702-f692de789727/page/BaCiD)




