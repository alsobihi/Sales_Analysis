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


#### أضرب عامود الكمية مع عامود سعر الحبة ليظهر الإجمالي





