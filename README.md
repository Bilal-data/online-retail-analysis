# online-retail-analysis
Revenue analysis of a UK online retailer (UCI Online Retail dataset)


Analysis of the transactions of a UK-based online retailer (1 Dec 2010 to 9 Dec 2011), done with Python (pandas) in Google Colab.

## Data

- UCI Machine Learning Repository, [Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail): 541,909 rows, 8 columns.
- License: CC BY 4.0. Citation: Chen, D. (2015). Online Retail [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33
- The data file is not included here. The notebook downloads it from UCI.

## Cleaning decisions

- 135,080 rows (about 25%) have no CustomerID and 1,454 have no Description.
- 10,624 rows have a negative quantity. 9,288 of them are cancellations (the invoice number starts with C). The other 1,336 have a unit price of 0 and no description or customer. They look like stock adjustments, but the data does not say.
- Gross view: only rows with quantity and price above 0 (530,104 rows, 11,805 removed).
- Net view: all rows with price above 0, so returns and cancellations are subtracted.

## Key findings

- UK customers bring 84.6% of gross revenue. Next: Netherlands 2.7%, EIRE 2.7%, Germany 2.1%, France 2.0%.
- Monthly net revenue peaks in November 2011 (1,461,756). September to November are far above the earlier months (about 0.5 to 0.75 million).
- The data ends on 9 Dec 2011 at 12:50, so December 2011 is incomplete. Comparing it with a full month is misleading.
- Same-period check (1 to 9 December): gross revenue looks 45.6% higher in 2011 (438,853 against 638,793). But one invoice (581483, 80,995 units of a single item, 168,470) was cancelled 12 minutes later (C581484). On a net basis the growth is 14.9% (377,488 against 433,668). Invoice counts were almost the same (834 and 819).
- Invoice size: the mean invoice is 845.7 outside the UK against 500.9 in the UK (medians 424.1 and 300.5). A permutation test (10,000 shuffles of invoices) gives p < 0.0001 for both differences, so it is very unlikely to be chance. I do not know the reason (wholesale buyers is my guess).
- Cancellations: 3,836 cancellation invoices worth 896,812, which is 8.4% of gross revenue.
- Customers: 4,338 customers have an ID. The top 10 bring 17.3% of their revenue and the top 20% bring 74.6%.

## Limitations

- Mostly descriptive analysis, with one statistical test (UK against other countries). Invoices of the same customer are not independent, and I could not shuffle by customer because 25% of rows have no CustomerID.
- The 14.9% comes from 9 days only, so it is a hint, not a conclusion.
- Customer-level analysis would cover only about 75% of rows (the ones with a CustomerID).
- I matched only one cancellation to its original invoice. Other cancellations may refer to earlier sales that I did not check.
- The net view still includes non-product lines such as discounts, because I only filtered on price.
- No cost or profit column, so this is revenue only. The data does not state the currency.


---

## بالعربي

تحليل معاملات متجر إنترنت بريطاني (من 1 ديسمبر 2010 لحد 9 ديسمبر 2011) باستخدام بايثون (pandas) في Google Colab.

### الداتا

- مستودع UCI للتعلم الآلي، داتا [Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail): 541,909 سطر و8 أعمدة.
- الترخيص: CC BY 4.0. المصدر: Chen, D. (2015). Online Retail [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33
- ملف الداتا مش موجود هنا. النوتبوك بينزّله من UCI.

### قرارات التنظيف

- 135,080 سطر (حوالي 25%) من غير CustomerID، و1,454 من غير Description.
- 10,624 سطر كميتهم سالبة. منهم 9,288 إلغاءات (رقم الفاتورة بيبدأ بحرف C). الـ 1,336 الباقيين سعرهم صفر ومفيش وصف ولا عميل. شكلهم تسويات مخزون، بس الداتا ما بتقولش.
- العرض الإجمالي (Gross): بس السطور اللي كميتها وسعرها أكبر من صفر (530,104 سطر، واتشال 11,805).
- العرض الصافي (Net): كل السطور اللي سعرها أكبر من صفر، فالمرتجعات والإلغاءات بتتخصم.

### أهم النتايج

- عملاء بريطانيا بيجيبوا 84.6% من الإيراد الإجمالي. بعدهم: هولندا 2.7% وأيرلندا (EIRE) 2.7% وألمانيا 2.1% وفرنسا 2.0%.
- الإيراد الصافي الشهري بيوصل لقمته في نوفمبر 2011 (1,461,756). من سبتمبر لنوفمبر أعلى بكتير من الشهور اللي قبلهم (حوالي 0.5 لـ 0.75 مليون).
- الداتا بتخلص يوم 9 ديسمبر 2011 الساعة 12:50، فشهر ديسمبر 2011 ناقص. مقارنته بشهر كامل بتضلل.
- مقارنة نفس الفترة (من 1 لـ 9 ديسمبر): الإيراد الإجمالي شكله أعلى 45.6% في 2011 (438,853 مقابل 638,793). لكن فاتورة واحدة (581483، 80,995 قطعة من صنف واحد، 168,470) اتلغت بعد 12 دقيقة (C581484). بالصافي النمو 14.9% (377,488 مقابل 433,668). وعدد الفواتير كان تقريبًا نفسه (834 و819).
- حجم الفاتورة: متوسط الفاتورة 845.7 برّه بريطانيا مقابل 500.9 في بريطانيا (الوسيط 424.1 و300.5). اختبار permutation (10,000 خلطة للفواتير) طلع p < 0.0001 للفرقين، يعني مستبعد جدًا يكون صدفة. السبب مش معروف (تجار جملة تخمين مني).
- الإلغاءات: 3,836 فاتورة إلغاء قيمتها 896,812، يعني 8.4% من الإيراد الإجمالي.
- العملاء: 4,338 عميل عندهم رقم. أكبر 10 بيجيبوا 17.3% من إيرادهم، وأكبر 20% بيجيبوا 74.6%.

### الحدود

- تحليل وصفي في الأساس، مع اختبار إحصائي واحد (بريطانيا مقابل باقي الدول). فواتير نفس العميل مش مستقلة، وما قدرتش أخلط على مستوى العميل لأن 25% من السطور من غير CustomerID.
- نسبة الـ 14.9% جاية من 9 أيام بس، فهي مؤشر مش استنتاج.
- أي تحليل على مستوى العميل هيغطي حوالي 75% من السطور بس (اللي فيها CustomerID).
- ربطت إلغاء واحد بس بفاتورته الأصلية. إلغاءات تانية ممكن تكون لمبيعات أقدم ما فحصتهاش.
- العرض الصافي لسه فيه سطور مش منتجات زي الخصومات، لأني فلترت بالسعر بس.
- مفيش عمود تكلفة أو ربح، فده إيراد بس. والداتا ما بتقولش العملة إيه.
