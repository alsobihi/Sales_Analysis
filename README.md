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


### الخطوة الثانية تنظيف البيانات

#### قم بحساب عدد الصفوف في الجدول

#### قم بحساب عدد الصفوف الفارغة `NULL`

#### قم بحذف الصفوف الفارغة
بعد الحدذف تأكد من ان عدد الصفوف مطابق للصفوف الفارغة واجمالي عدد الصفوف الحالي 



### قم بحذف الصفوف المتكررة



