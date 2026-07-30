<p align="center"><b>العربية</b> · <a href="#english-version">English</a></p>

# تحليل مبيعات Superstore

تحليل شامل لبيانات Superstore المعروفة، نحو 9,994 طلب، من أوله إلى آخره: تنظيف في Python، ثم تحليل بـSQL، ثم لوحة Power BI مبنية فوقهما. الهدف واضح، وهو معرفة ما الذي يحقّق الربح لهذا النشاط فعليًا، وأين يخسر دون أن يُلاحَظ.

![لوحة Power BI](dashboard_preview.png)

## أبرز النتائج

قطاع التقنية هو المحرّك، إذ يتصدّر المبيعات (836 ألف$) والربح (145 ألف$). الأثاث هو الاستثناء اللافت: يبيع بقدر المستلزمات المكتبية تقريبًا، لكنه لا يحقّق سوى 18 ألف$ ربحًا، أي بهامش 2.5% فقط. وعند البحث في السبب تبيّن أنه الخصومات؛ فأي منتج يُخفَّض أكثر من 30% يميل إلى الخسارة، والطلبات في شريحة 30% إلى 50% خصم تخسر نحو 156$ لكل طلب، وهو ما يفسّر ضعف أرقام الأثاث.

المناطق تحكي القصة نفسها. الغرب هو الأصحّ بهامش 14.9%، بينما يبيع الوسط أكثر من الجنوب لكنه يحتفظ بربح أقل (7.9%)، وهذا غالبًا مؤشر على مشكلة تسعير أو خصم لا ضعف طلب. ترتفع المبيعات في نوفمبر وديسمبر وتنخفض بوضوح في فبراير. ولمن يوازن بين السرعة والتكلفة، يستغرق الشحن العادي نحو خمسة أيام مقابل يومين وربع للشحن السريع.

## كيف بُني

بدأ العمل بالتنظيف في Python باستخدام pandas: ضبط أعمدة التاريخ، وإضافة عمود للشهر وآخر لمدة الشحن، والتأكّد من خلوّ الـ9,994 صف من الفراغات والتكرار. بعد ذلك أُجيبت الأسئلة نفسها مرتين، مرة في Python ومرة في SQL، ليتحقّق كل طريق من نتائج الآخر.

الأدوات: Python (pandas وNumPy)، وSQL (SQLite)، وPower BI، وExcel للبيانات المصدر.

## الداشبوردات الثلاثة

النتائج نفسها معروضة بثلاث صيغ، ولكل واحدة دورها:

**Power BI** هي الأساسية. مبنية على نموذج نجمي صغير (عميل، تاريخ، منتج، جغرافيا، طريقة شحن)، وهي الأداة التي تُستخدم فعليًا للتصفية وقراءة الأرقام منها. نموذج بياناتها في مجلد `powerbi/`.

**Excel** تقدّم التحليل نفسه لمن يفضّل الجداول، عبر PivotTables وSlicers.

**نسخة الويب** غرضها العرض لا التحليل. صفحة واحدة متحركة تستعرض النتائج، أقرب إلى بوستر منها إلى أداة. التحليل الفعلي والأرقام في ملف Power BI، وهذه طريقة أوضح لعرضها بصريًا.

![الداشبورد الويب](dashboards/web_dashboard_preview.png)

## محتويات الريبو

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

A full analysis of the well-known Superstore dataset, about 9,994 orders, taken from start to finish: cleaned in Python, explored in SQL, and built into a Power BI dashboard. The goal was straightforward, to understand what actually makes this business money and where it loses it without anyone noticing.

![Power BI dashboard](dashboard_preview.png)

## Key findings

Technology is the engine of the business, leading on both sales ($836K) and profit ($145K). Furniture is the notable exception: it sells almost as much as Office Supplies, yet returns only $18K in profit, a margin of just 2.5%. Looking into why, the cause was discounts. Anything marked down more than 30% tends to lose money, and orders in the 30% to 50% range lose roughly $156 each, which explains most of Furniture's weak numbers.

The regions tell the same story. The West is the healthiest at a 14.9% margin, while Central sells more than the South but keeps less of it (7.9%), which usually signals a pricing or discount problem rather than weak demand. Sales rise in November and December and fall noticeably in February. And for anyone weighing speed against cost, Standard shipping takes about five days versus 2.2 for First Class.

## How it was built

The work began with cleaning in Python using pandas: fixing the date columns, adding an order-month field and a shipping-duration field, and confirming the 9,994 rows held no nulls or duplicates. The same questions were then answered twice, once in Python and once in SQL, so each could verify the other.

Tools: Python (pandas, NumPy), SQL (SQLite), Power BI, and Excel for the source data.

## The three dashboards

The same findings appear in three formats, each with its own purpose:

**Power BI** is the primary one. It sits on a small star schema (customer, date, product, geography, ship mode) and is the tool you would actually use to filter and read the numbers. Its data model is in the `powerbi/` folder.

**Excel** offers the same analysis for those who prefer a spreadsheet, using PivotTables and slicers.

**The web version** is meant for viewing rather than analysis. It is a single animated page that presents the findings, closer to a poster than a tool. The real analysis and the numbers live in the Power BI file; this is simply a clearer way to show them visually.

![Web dashboard](dashboards/web_dashboard_preview.png)

## What's in the repo

- `01_data_cleaning.ipynb` — cleaning and exploratory analysis in Python
- `superstore_queries.sql` — the SQL business questions
- `Superstore Sales Performance Dashboard.pbix` — the Power BI dashboard
- `powerbi/` — the star-schema data model
- `dashboards/` — the Excel and web versions
- `data/processed/` — the summarized tables
- `docs/` — data model and design notes
