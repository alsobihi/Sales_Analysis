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

#### قم بحساب عدد الصفوف الفارغة `NULL`

#### قم بحذف الصفوف الفارغة
بعد الحدذف تأكد من ان عدد الصفوف مطابق للصفوف الفارغة واجمالي عدد الصفوف الحالي 


#### قم بحساب الصفوف المتكررة

#### قم بحذف الصفوف المتكررة

### الخطوة الثالثة تحويل البيانات


#### أضف عامود جديد بأسم `Month` وضع أسم الشهر المناسب في كل صف


#### أضف عامود جديد بأسم  `Country` وضع فيه أسم الدولة USA



#### أضف عامود جديد بأسم  `City` وضع فيه أسم مدينة العميل


#### أضرب عامود الكمية مع عامود سعر الحبة ليظهر الإجمالي





