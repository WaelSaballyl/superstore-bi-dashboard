<p align="center"><b>العربية</b> · <a href="#english-version">English</a></p>

# تحليل مبيعات Superstore

أخذت بيانات Superstore المعروفة، حوالي 9,994 طلب، وسوّيت عليها التحليل من أوله لآخره. نظّفتها في Python، حلّلتها بـSQL، وبنيت فوقها لوحة Power BI. الفكرة بسيطة: أعرف وش اللي يربّح هالنشاط فعليًا، ووين يخسر بدون ما ينتبه أحد.

![لوحة Power BI](dashboard_preview.png)

## أهم النتائج

قطاع التقنية هو المحرّك، الأول في المبيعات (836 ألف$) والأول في الربح (145 ألف$). الأثاث هو الاستثناء الغريب. يبيع تقريبًا مثل المستلزمات المكتبية، بس ما يجمع إلا 18 ألف$ ربح، يعني هامش 2.5% فقط. ولمّا بحثت عن السبب طلعت الخصومات: أي منتج مخفّض أكثر من 30% يميل للخسارة، والطلبات بين 30% و50% خصم تخسر حوالي 156$ لكل طلب. وهذا لحاله يفسّر ضعف أرقام الأثاث.

المناطق نفس الحكاية. الغرب هو الأصحّ بهامش 14.9%. الوسط لافت للنظر، يبيع أكثر من الجنوب لكن يحتفظ بربح أقل (7.9%)، وغالبًا هذا مؤشر مشكلة تسعير أو خصم، مو ضعف طلب. المبيعات ترتفع كل نوفمبر وديسمبر وتنزل بشدة في فبراير. ولو أحد يوازن بين السرعة والتكلفة، الشحن العادي ياخذ حوالي خمسة أيام مقابل يومين وربع للسريع.

## كيف بنيته

التنظيف أول، في Python بـpandas. ظبّطت أعمدة التاريخ، أضفت عمود الشهر وعمود مدة الشحن، وتأكّدت ما فيه فراغات ولا تكرار مختبّي بين الـ9,994 صف. بعدها جاوبت نفس الأسئلة مرتين، مرة بـPython ومرة بـSQL، عشان كل وحدة تصير تحقّق للثانية.

الأدوات: Python (pandas وNumPy)، وSQL (SQLite)، وPower BI، وExcel للبيانات المصدر.

## الثلاث داشبوردات

نفس النتائج بثلاث صيغ، ويهمّك تعرف كل وحدة لايش.

**Power BI** هي الأساسية. قاعدة على نموذج نجمي صغير (عميل، تاريخ، منتج، جغرافيا، طريقة شحن)، وهي اللي تستخدمها فعليًا: تفلتر وتقرأ الأرقام منها. نموذج بياناتها في مجلد `powerbi/`.

**Excel** نفس التحليل بس لأهل الجداول، بـPivotTables وSlicers.

**نسخة الويب** موجودة عشان تتفرّج عليها، مو عشان تشتغل بها. صفحة متحركة وحدة تمشّيك على النتائج، أقرب لبوستر منها لأداة. التحليل الحقيقي والأرقام في ملف Power BI، وهذي بس طريقة أحلى للعرض.

![الداشبورد الويب](dashboards/web_dashboard_preview.png)

## وش في الريبو

- `01_data_cleaning.ipynb` — التنظيف والاستكشاف في Python
- `superstore_queries.sql` — أسئلة العمل بـSQL
- `Superstore Sales Performance Dashboard.pbix` — لوحة Power BI
- `powerbi/` — نموذج البيانات النجمي
- `dashboards/` — نسختا Excel والويب
- `data/processed/` — الجداول الملخّصة
- `docs/` — ملاحظات النموذج والتصميم

---

<a id="english-version"></a>
<p align="center"><a href="#تحليل-مبيعات-superstore">العربية</a> · <b>English</b></p>

# Superstore Sales Analysis

I took the classic Superstore dataset, about 9,994 orders, and ran it start to finish. Cleaned it in Python, dug into it with SQL, and built a Power BI dashboard on top. The goal was simple: figure out what actually makes this business money, and where it quietly loses it.

![Power BI dashboard](dashboard_preview.png)

## What I found

Technology is the workhorse. It comes first in sales ($836K) and first in profit ($145K). Furniture is the odd one out. It sells almost as much as Office Supplies but only clears $18K in profit, which is a 2.5% margin. When I dug into why, the answer was discounts. Anything marked down more than 30% tends to lose money, and orders in the 30 to 50% range lose around $156 each on average. That alone explains most of Furniture's weak numbers.

The regions tell a similar story. The West is the healthy one at a 14.9% margin. Central is the interesting case: it outsells the South but keeps less of the money (7.9%), which usually points to a pricing or discount problem rather than weak demand. Sales climb every November and December and drop off in February. And for anyone weighing speed against cost, Standard shipping runs about five days versus 2.2 for First Class.

## How I built it

Cleaning came first, in Python with pandas. I fixed the date columns, added an order-month field and a shipping-duration field, and made sure nothing was hiding in the 9,994 rows, no nulls or duplicates. Then I answered the same questions twice, once in Python and once in SQL, so each one could double as a check on the other.

Tools: Python (pandas, NumPy), SQL (SQLite), Power BI, and Excel for the source data.

## The three dashboards

Same findings, three formats. It helps to know what each one is actually for.

**Power BI** is the real one. It sits on a small star schema (customer, date, product, geography, ship mode) and it's what you'd genuinely use day to day, filtering it and reading the numbers off it. Its data model is in the `powerbi/` folder.

**Excel** is the same analysis for spreadsheet people, done with PivotTables and slicers.

**The web version** is there to be looked at, not used. It's a single animated page that walks through the findings, more of a poster than a tool. The real analysis lives in the Power BI file. This is just a nicer way to show it off.

![Web dashboard](dashboards/web_dashboard_preview.png)

## What's in the repo

- `01_data_cleaning.ipynb` — cleaning and exploratory analysis in Python
- `superstore_queries.sql` — the SQL business questions
- `Superstore Sales Performance Dashboard.pbix` — the Power BI dashboard
- `powerbi/` — the star-schema data model
- `dashboards/` — the Excel and web versions
- `data/processed/` — the summarized tables
- `docs/` — data model and design notes
