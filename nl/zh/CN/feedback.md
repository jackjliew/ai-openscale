---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: feedback data, data, feedback, models

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# 在 {{site.data.keyword.aios_short}} 中格式化和上载反馈数据
{: #fmt-upld-fdbk-data}

反馈数据对于维护无偏差模型至关重要。必须定期将反馈数据上载到 {{site.data.keyword.aios_full}} 服务，以确保模型将可能指示预测性应用程序上下文中的更改的最新数据考虑在内。借助反馈过程，系统通过监视预测的有效性并在需要时重新训练来持续学习。监视和使用生成的反馈是机器学习的核心所在。以下信息旨在帮助您格式化和上载反馈数据。
(: shortdesc)

## 格式化反馈数据
{: #fmt-upld-fdbk-data-fmt}

要正确读取反馈数据，必须正确将其格式化。{{site.data.keyword.aios_short}} 服务接受以下格式：

- CSV 文件格式，可以通过使用 UI 或 REST API 进行上载
- JSON 文件格式，只能通过使用 REST API 进行上载

这些文件格式由可在预订详细信息中获取的模式 `training_data_schema` 来定义。要查看 `training_data_schema`，请使用 Python API 运行以下命令：

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

要将训练数据模式与反馈模式进行比较，可能也要查看反馈模式。要查看反馈模式，请使用 Python API 运行以下命令：

```
subscription.feedback_logging.print_table_schema()
```


### CSV 格式
{: #fmt-upld-fdbk-data-fmt-csv}

通常对于 CSV 文件而言，您在列和行中提供数据，其中一行表示列名。

在列名为全大写时无需双引号 (")，这使其对于 Db2 而言不区分大小写，但是对于其他数据库以及在列名采用混合大小写的情况下，大小写必须匹配。
 
反馈 CSV 文件预计具有所有特征值以及手动分配的目标/标签值。例如，药品模型训练数据包含特征值 `AGE`、`SEX`、`BP`、`CHOLESTEROL`、`NA`、`K` 和目标/标签值 `DRUG`。反馈 CSV 文件需要包含这些字段的值；例如 `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`。如果为反馈 CSV 文件提供了标题，那么将使用该标题来映射字段名称。否则，字段顺序**必须**与训练模式中的顺序完全相同。
有关训练数据的更多信息，请参阅 [ 为什么 {{site.data.keyword.aios_short}} 需要访问我的培训数据？](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) 

请注意，模型返回的预测类型与反馈数据中的标签/目标列必须匹配。
{: note}

文件大小当前限制为 8 MB。
{: note}

如果文件包含列名，那么列未必一定与表顺序匹配，但是，如果文件没有任何列名，那么必须与表顺序匹配。可以具有原始训练数据中未包含的列。在处理期间会忽略这些列。以下样本显示有效格式化的 CSV 格式文件，其中对列名使用了双引号 (")：

```
"CheckingStatus","LoanDuration","CreditHistory","LoanPurpose","LoanAmount","ExistingSavings","EmploymentDuration","InstallmentPercent","Sex","OthersOnLoan","CurrentResidenceDuration","OwnsProperty","Age","InstallmentPlans","Housing","ExistingCreditsCount","Job","Dependents","Telephone","ForeignWorker","Risk"
no_checking,28,outstanding_credit,appliances,5990,500_to_1000,greater_7,5,male,co-applicant,3,car_other,55,none,free,2,skilled,2,yes,yes,Risk
greater_200,22,all_credits_paid_back,car_used,3376,less_100,less_1,3,female,none,2,car_other,32,none,own,1,skilled,1,none,yes,No Risk
no_checking,39,credits_paid_to_date,vacation,6434,unknown,greater_7,5,male,none,4,car_other,39,none,own,2,skilled,2,yes,yes,Risk
0_to_200,20,credits_paid_to_date,furniture,2442,less_100,unemployed,3,female,none,1,real_estate,42,none,own,1,skilled,1,none,yes,No Risk
greater_200,4,all_credits_paid_back,education,4206,less_100,unemployed,1,female,none,3,savings_insurance,27,none,own,1,management_self-employed,1,none,yes,No Risk
greater_200,23,credits_paid_to_date,car_used,2963,greater_1000,greater_7,4,male,none,4,car_other,46,none,own,2,skilled,1,none,yes,Risk
no_checking,31,prior_payments_delayed,vacation,2673,500_to_1000,1_to_4,3,male,none,2,real_estate,35,stores,rent,1,skilled,2,none,yes,Risk
no_checking,37,prior_payments_delayed,other,6971,500_to_1000,1_to_4,3,male,none,3,savings_insurance,54,none,own,2,skilled,1,yes,yes,Risk
no_checking,14,all_credits_paid_back,car_new,1525,500_to_1000,4_to_7,3,male,none,4,real_estate,33,none,own,1,skilled,1,none,yes,No Risk
less_0,10,prior_payments_delayed,furniture,4037,less_100,4_to_7,3,male,none,3,savings_insurance,31,none,rent,1,skilled,1,none,yes,Risk
0_to_200,28,credits_paid_to_date,retraining,1152,less_100,less_1,2,female,none,2,savings_insurance,20,stores,own,1,skilled,1,none,yes,No Risk
less_0,17,credits_paid_to_date,car_new,1880,less_100,less_1,3,female,co-applicant,2,savings_insurance,41,none,own,1,skilled,1,none,yes,No Risk
0_to_200,39,prior_payments_delayed,appliances,5685,100_to_500,1_to_4,4,female,none,2,unknown,37,none,own,2,skilled,1,yes,yes,Risk
no_checking,32,prior_payments_delayed,radio_tv,5105,500_to_1000,1_to_4,4,male,none,5,savings_insurance,44,none,own,2,management_self-employed,1,none,yes,Risk
no_checking,38,prior_payments_delayed,appliances,4990,500_to_1000,greater_7,4,male,none,4,car_other,50,bank,own,2,unemployed,2,yes,yes,Risk
less_0,17,credits_paid_to_date,furniture,1017,less_100,less_1,2,female,none,1,car_other,30,none,own,1,skilled,1,none,yes,No Risk
less_0,33,all_credits_paid_back,car_new,3618,500_to_1000,4_to_7,2,male,none,3,unknown,31,stores,own,2,unskilled,1,none,yes,No Risk
less_0,12,no_credits,car_new,3037,less_100,less_1,1,female,none,2,car_other,31,stores,own,1,skilled,1,none,yes,No Risk
no_checking,23,prior_payments_delayed,furniture,1440,100_to_500,1_to_4,3,female,none,3,real_estate,39,stores,own,1,unskilled,1,yes,yes,No Risk
less_0,18,prior_payments_delayed,retraining,4032,less_100,1_to_4,2,female,none,2,car_other,36,none,rent,1,skilled,1,none,yes,No Risk
```

### JSON 格式
{: #fmt-upld-fdbk-data-fmt-json}

JSON 格式由字段与列名对应的对象集合组成。以下样本显示完整的有效格式化的 JSON 格式文件：


```
{ "data":
[
["less_0",10,"all_credits_paid_back","car_new",250,"500_to_1000","4_to_7",3,"male","none",2,"real_estate",23,"none","rent",1,"skilled",1,"none","yes","No Risk"],
["no_checking",23,"prior_payments_delayed","appliances",6964,"100_to_500","4_to_7",4,"female","none",3,"car_other",39,"none","own",1,"skilled",1,"none","yes","Risk"],
["0_to_200",30,"outstanding_credit","appliances",3464,"100_to_500","greater_7",3,"male","guarantor",4,"savings_insurance",51,"stores","free",1,"skilled",1,"yes","yes","Risk"],
["no_checking",23,"outstanding_credit","car_used",2681,"500_to_1000","greater_7",4,"male","none",3,"car_other",33,"stores","free",1,"unskilled",1,"yes","yes","No Risk"],
["0_to_200",18,"prior_payments_delayed","furniture",1673,"less_100","1_to_4",2,"male","none",3,"car_other",30,"none","own",2,"skilled",1,"none","yes","Risk"],
["no_checking",44,"outstanding_credit","radio_tv",3476,"unknown","greater_7",4,"male","co-applicant",4,"unknown",60,"none","free",2,"skilled",2,"yes","yes","Risk"],
["less_0",8,"no_credits","education",803,"less_100","unemployed",1,"male","none",1,"savings_insurance",19,"stores","rent",1,"skilled",1,"none","yes","No Risk"],
["0_to_200",7,"all_credits_paid_back","car_new",250,"less_100","unemployed",1,"male","none",1,"real_estate",19,"stores","rent",1,"skilled",1,"none","yes","No Risk"],
["0_to_200",33,"credits_paid_to_date","radio_tv",3548,"100_to_500","1_to_4",3,"male","none",4,"car_other",28,"none","own",2,"skilled",1,"yes","yes","Risk"],
["no_checking",24,"prior_payments_delayed","retraining",4158,"100_to_500","greater_7",3,"female","none",2,"savings_insurance",35,"stores","own",1,"unskilled",2,"none","yes","Risk"],
["no_checking",30,"prior_payments_delayed","appliances",5796,"unknown","4_to_7",4,"male","none",4,"car_other",49,"none","own",2,"management_self-employed",2,"none","yes","No Risk"],
["0_to_200",6,"prior_payments_delayed","furniture",2079,"500_to_1000","less_1",3,"female","none",3,"savings_insurance",35,"none","rent",1,"skilled",1,"none","yes","No Risk"],
["0_to_200",16,"credits_paid_to_date","car_new",4172,"less_100","4_to_7",3,"male","none",3,"savings_insurance",30,"none","own",1,"skilled",1,"yes","yes","No Risk"],
["no_checking",31,"outstanding_credit","appliances",9149,"unknown","greater_7",5,"male","co-applicant",3,"unknown",61,"none","own",3,"skilled",2,"yes","yes","Risk"],
["no_checking",28,"outstanding_credit","appliances",7653,"unknown","4_to_7",4,"male","none",5,"car_other",42,"none","own",2,"skilled",1,"none","yes","No Risk"],
["0_to_200",14,"credits_paid_to_date","furniture",2056,"less_100","4_to_7",3,"male","none",3,"real_estate",20,"none","rent",1,"skilled",1,"none","yes","No Risk"],
["no_checking",29,"prior_payments_delayed","appliances",4321,"greater_1000","4_to_7",4,"male","none",4,"savings_insurance",39,"none","free",2,"management_self-employed",1,"yes","yes","Risk"],
["no_checking",8,"prior_payments_delayed","car_new",3332,"greater_1000","greater_7",3,"male","none",2,"savings_insurance",43,"none","free",2,"skilled",1,"yes","yes","Risk"],
["0_to_200",28,"credits_paid_to_date","furniture",3021,"less_100","4_to_7",3,"male","none",2,"savings_insurance",32,"none","own",2,"skilled",1,"none","yes","No Risk"],
["0_to_200",4,"prior_payments_delayed","car_new",250,"less_100","4_to_7",2,"male","none",2,"car_other",52,"bank","rent",1,"unemployed",1,"yes","yes","No Risk"],
["0_to_200",24,"outstanding_credit","business",5245,"100_to_500","greater_7",4,"male","none",4,"unknown",40,"none","own",2,"management_self-employed",1,"none","yes","Risk"],
["less_0",4,"all_credits_paid_back","radio_tv",1104,"less_100","1_to_4",2,"male","none",1,"savings_insurance",21,"none","rent",1,"skilled",1,"none","yes","No Risk"],
["less_0",10,"prior_payments_delayed","car_new",250,"less_100","4_to_7",3,"male","none",2,"real_estate",26,"none","own",1,"skilled",1,"none","yes","No Risk"],
["less_0",6,"all_credits_paid_back","radio_tv",250,"less_100","less_1",1,"female","none",2,"real_estate",19,"none","own",1,"skilled",1,"none","yes","No Risk"],
["no_checking",40,"outstanding_credit","education",7277,"unknown","greater_7",4,"male","co-applicant",5,"car_other",49,"none","own",2,"skilled",2,"yes","yes","Risk"],
["less_0",23,"credits_paid_to_date","repairs",1348,"500_to_1000","1_to_4",3,"male","none",2,"savings_insurance",35,"bank","own",2,"unskilled",1,"yes","yes","No Risk"],
["no_checking",31,"prior_payments_delayed","car_used",5011,"100_to_500","1_to_4",3,"male","none",3,"savings_insurance",41,"stores","own",1,"unskilled",1,"yes","no","No Risk"],
["0_to_200",21,"credits_paid_to_date","car_new",1658,"less_100","less_1",2,"male","none",3,"savings_insurance",27,"none","own",2,"skilled",1,"yes","yes","Risk"],
["no_checking",43,"prior_payments_delayed","appliances",6744,"greater_1000","4_to_7",3,"male","co-applicant",5,"savings_insurance",35,"none","own",2,"skilled",1,"none","yes","No Risk"],
["less_0",4,"all_credits_paid_back","car_used",250,"less_100","less_1",1,"female","none",2,"real_estate",22,"none","rent",1,"skilled",1,"none","yes","No Risk"],
["0_to_200",24,"credits_paid_to_date","car_used",3294,"less_100","less_1",3,"male","none",4,"real_estate",25,"none","own",1,"management_self-employed",1,"none","no","No Risk"],
["greater_200",17,"credits_paid_to_date","car_new",3581,"less_100","1_to_4",2,"male","none",4,"savings_insurance",25,"none","own",1,"skilled",1,"yes","yes","No Risk"],
["no_checking",52,"outstanding_credit","appliances",9249,"unknown","greater_7",5,"male","co-applicant",4,"unknown",52,"none","free",3,"skilled",2,"yes","yes","Risk"],
["0_to_200",15,"prior_payments_delayed","retraining",398,"less_100","less_1",2,"male","co-applicant",2,"savings_insurance",44,"none","own",1,"skilled",1,"yes","yes","No Risk"],
["0_to_200",26,"credits_paid_to_date","car_used",3650,"less_100","1_to_4",3,"male","none",4,"savings_insurance",32,"stores","own",1,"unskilled",1,"none","yes","Risk"],
["less_0",4,"credits_paid_to_date","car_new",250,"100_to_500","less_1",1,"female","none",1,"real_estate",19,"bank","rent",1,"unskilled",1,"none","yes","No Risk"],
["0_to_200",16,"credits_paid_to_date","furniture",1694,"100_to_500","4_to_7",3,"female","none",3,"savings_insurance",37,"none","own",2,"skilled",1,"none","yes","No Risk"],
["no_checking",48,"outstanding_credit","education",10197,"500_to_1000","4_to_7",4,"male","co-applicant",3,"unknown",36,"none","free",2,"skilled",1,"yes","yes","Risk"],
["no_checking",43,"prior_payments_delayed","repairs",5648,"unknown","greater_7",4,"male","co-applicant",5,"unknown",49,"none","own",3,"skilled",2,"yes","yes","Risk"],
["0_to_200",13,"prior_payments_delayed","radio_tv",2217,"greater_1000","1_to_4",3,"male","co-applicant",4,"unknown",46,"bank","own",1,"unemployed",1,"yes","no","Risk"],
["greater_200",24,"credits_paid_to_date","car_used",6428,"less_100","4_to_7",4,"female","none",4,"car_other",54,"none","own",1,"skilled",1,"yes","yes","Risk"],
["0_to_200",12,"no_credits","car_new",250,"less_100","less_1",2,"female","none",1,"real_estate",20,"bank","rent",1,"unskilled",1,"none","yes","No Risk"],
["0_to_200",24,"outstanding_credit","radio_tv",9282,"500_to_1000","1_to_4",4,"male","none",5,"car_other",32,"none","own",2,"management_self-employed",1,"none","yes","No Risk"],
["less_0",8,"no_credits","radio_tv",250,"less_100","unemployed",1,"male","none",1,"real_estate",19,"bank","rent",1,"unemployed",1,"none","yes","No Risk"],
["no_checking",25,"prior_payments_delayed","radio_tv",5159,"100_to_500","1_to_4",3,"male","none",4,"car_other",53,"none","own",1,"management_self-employed",2,"yes","yes","Risk"],
["less_0",4,"credits_paid_to_date","car_new",250,"less_100","unemployed",1,"male","co-applicant",2,"real_estate",31,"stores","own",1,"skilled",1,"none","yes","No Risk"],
["no_checking",25,"outstanding_credit","business",6725,"500_to_1000","4_to_7",3,"male","none",4,"unknown",50,"none","own",2,"skilled",2,"yes","yes","Risk"],
["no_checking",19,"outstanding_credit","car_used",5092,"500_to_1000","4_to_7",4,"male","none",5,"savings_insurance",38,"none","own",1,"management_self-employed",1,"yes","yes","No Risk"],
["0_to_200",26,"all_credits_paid_back","furniture",3635,"less_100","4_to_7",4,"male","co-applicant",2,"car_other",35,"none","free",2,"skilled",1,"yes","yes","Risk"],
["0_to_200",30,"credits_paid_to_date","radio_tv",1638,"500_to_1000","1_to_4",2,"female","none",1,"savings_insurance",21,"stores","rent",1,"skilled",1,"none","yes","Risk"],
["no_checking",30,"outstanding_credit","furniture",7499,"unknown","greater_7",5,"male","co-applicant",5,"car_other",60,"none","free",2,"skilled",2,"yes","yes","Risk"],
["greater_200",5,"credits_paid_to_date","car_new",1674,"less_100","less_1",3,"female","co-applicant",3,"real_estate",31,"none","own",1,"skilled",1,"yes","yes","No Risk"],
["less_0",16,"credits_paid_to_date","car_new",250,"less_100","4_to_7",2,"male","none",1,"real_estate",29,"stores","free",1,"unskilled",1,"none","yes","No Risk"],
["less_0",32,"outstanding_credit","appliances",3511,"100_to_500","4_to_7",4,"male","none",2,"car_other",24,"none","own",1,"skilled",1,"yes","yes","No Risk"],
["0_to_200",24,"outstanding_credit","appliances",4511,"100_to_500","greater_7",4,"male","none",4,"unknown",46,"none","own",1,"skilled",1,"none","no","No Risk"],
["less_0",4,"prior_payments_delayed","car_used",1394,"less_100","1_to_4",3,"female","none",1,"savings_insurance",28,"none","own",1,"skilled",1,"none","yes","No Risk"],
["0_to_200",23,"credits_paid_to_date","radio_tv",2795,"less_100","1_to_4",3,"male","none",3,"car_other",29,"none","own",1,"skilled",1,"none","yes","No Risk"],
["no_checking",17,"credits_paid_to_date","retraining",4331,"less_100","less_1",3,"male","none",3,"savings_insurance",32,"none","free",1,"management_self-employed",1,"none","yes","No Risk"],
["0_to_200",16,"prior_payments_delayed","radio_tv",2373,"less_100","1_to_4",3,"female","none",1,"savings_insurance",32,"none","free",2,"skilled",1,"none","yes","No Risk"],
["no_checking",38,"prior_payments_delayed","furniture",8742,"500_to_1000","4_to_7",3,"male","co-applicant",4,"unknown",46,"none","free",2,"skilled",1,"yes","yes","Risk"],
["greater_200",28,"prior_payments_delayed","radio_tv",3936,"100_to_500","1_to_4",4,"male","none",4,"car_other",36,"none","free",2,"management_self-employed",1,"yes","yes","No Risk"],
["less_0",24,"prior_payments_delayed","furniture",5098,"less_100","4_to_7",4,"female","none",2,"car_other",39,"none","own",2,"skilled",1,"none","yes","Risk"],
["no_checking",27,"prior_payments_delayed","furniture",5250,"100_to_500","1_to_4",4,"male","none",2,"car_other",53,"none","own",2,"skilled",1,"yes","yes","Risk"],
["less_0",4,"all_credits_paid_back","car_used",250,"less_100","1_to_4",1,"female","none",2,"real_estate",25,"stores","rent",1,"skilled",1,"none","yes","No Risk"],
["less_0",14,"prior_payments_delayed","vacation",4398,"less_100","1_to_4",3,"male","none",3,"car_other",31,"none","own",2,"skilled",1,"none","yes","No Risk"],
["0_to_200",4,"all_credits_paid_back","car_new",250,"less_100","1_to_4",2,"female","none",1,"real_estate",42,"none","own",1,"skilled",1,"none","yes","No Risk"],
["less_0",16,"credits_paid_to_date","furniture",2291,"less_100","less_1",3,"male","none",2,"savings_insurance",32,"stores","rent",1,"unskilled",1,"none","yes","No Risk"],
["no_checking",31,"prior_payments_delayed","furniture",7079,"100_to_500","less_1",4,"female","none",3,"car_other",43,"none","own",2,"skilled",2,"yes","yes","No Risk"],
["0_to_200",14,"credits_paid_to_date","car_new",4366,"100_to_500","1_to_4",3,"female","none",1,"car_other",37,"none","own",1,"skilled",1,"none","yes","No Risk"],
["no_checking",17,"credits_paid_to_date","repairs",3418,"100_to_500","less_1",2,"male","none",4,"car_other",43,"stores","own",2,"unskilled",1,"none","yes","Risk"],
["less_0",20,"credits_paid_to_date","furniture",902,"less_100","4_to_7",2,"male","none",1,"savings_insurance",26,"stores","own",1,"unskilled",1,"none","no","No Risk"],
["less_0",4,"credits_paid_to_date","car_used",250,"500_to_1000","less_1",1,"female","none",1,"real_estate",19,"stores","own",1,"unskilled",1,"none","yes","No Risk"],
["0_to_200",17,"no_credits","car_new",1662,"less_100","less_1",2,"female","none",2,"savings_insurance",32,"none","own",2,"skilled",1,"yes","yes","No Risk"],
["0_to_200",27,"credits_paid_to_date","education",1272,"greater_1000","1_to_4",3,"male","none",2,"savings_insurance",37,"stores","own",2,"unskilled",1,"none","no","No Risk"],
["less_0",14,"prior_payments_delayed","radio_tv",1640,"500_to_1000","less_1",2,"male","none",2,"real_estate",29,"none","rent",2,"skilled",1,"none","yes","No Risk"],
["greater_200",20,"credits_paid_to_date","car_new",250,"100_to_500","1_to_4",2,"male","none",3,"savings_insurance",44,"none","own",1,"skilled",1,"yes","yes","No Risk"],
["no_checking",33,"all_credits_paid_back","education",6126,"less_100","4_to_7",5,"male","none",3,"savings_insurance",33,"stores","rent",1,"unskilled",1,"none","yes","Risk"],
["0_to_200",8,"prior_payments_delayed","car_new",731,"greater_1000","1_to_4",3,"female","none",2,"savings_insurance",33,"bank","rent",1,"unemployed",2,"none","yes","No Risk"],
["no_checking",31,"prior_payments_delayed","vacation",5086,"100_to_500","greater_7",5,"male","none",3,"savings_insurance",44,"none","free",2,"management_self-employed",1,"none","yes","Risk"],
["less_0",15,"prior_payments_delayed","furniture",3986,"less_100","less_1",2,"male","none",2,"car_other",19,"bank","rent",1,"unskilled",1,"none","yes","No Risk"],
["0_to_200",13,"credits_paid_to_date","car_new",1700,"less_100","4_to_7",3,"female","none",2,"car_other",39,"none","own",1,"skilled",1,"none","yes","Risk"],
["0_to_200",4,"all_credits_paid_back","car_new",250,"less_100","1_to_4",2,"female","none",1,"real_estate",29,"none","own",1,"skilled",1,"none","yes","No Risk"],
["less_0",16,"prior_payments_delayed","car_new",2056,"less_100","4_to_7",2,"male","none",2,"unknown",34,"stores","own",1,"skilled",1,"none","yes","No Risk"],
["no_checking",32,"prior_payments_delayed","car_used",5145,"500_to_1000","4_to_7",4,"male","none",4,"savings_insurance",40,"none","own",1,"skilled",1,"none","yes","No Risk"],
["greater_200",24,"outstanding_credit","business",8570,"100_to_500","4_to_7",4,"male","none",4,"unknown",47,"none","own",2,"skilled",1,"yes","yes","Risk"],
["no_checking",16,"all_credits_paid_back","vacation",2928,"less_100","1_to_4",2,"female","none",1,"real_estate",29,"none","own",1,"management_self-employed",1,"none","yes","No Risk"],
["less_0",25,"credits_paid_to_date","car_new",2049,"less_100","less_1",2,"male","none",1,"real_estate",33,"none","own",1,"skilled",1,"none","yes","No Risk"],
["no_checking",24,"prior_payments_delayed","car_used",3838,"500_to_1000","1_to_4",4,"female","none",3,"savings_insurance",41,"none","own",2,"skilled",1,"none","yes","No Risk"],
["0_to_200",21,"all_credits_paid_back","car_new",1653,"100_to_500","less_1",1,"female","none",1,"car_other",33,"bank","rent",1,"unemployed",1,"none","yes","No Risk"],
["less_0",7,"credits_paid_to_date","car_new",250,"less_100","1_to_4",1,"female","none",2,"savings_insurance",19,"stores","rent",1,"skilled",1,"none","yes","No Risk"],
["0_to_200",20,"credits_paid_to_date","retraining",2553,"less_100","1_to_4",3,"female","none",3,"savings_insurance",27,"stores","rent",1,"unskilled",2,"none","yes","No Risk"],
["less_0",39,"prior_payments_delayed","appliances",820,"100_to_500","4_to_7",2,"male","none",1,"savings_insurance",26,"stores","own",1,"skilled",1,"none","yes","No Risk"],
["0_to_200",20,"credits_paid_to_date","retraining",2810,"less_100","1_to_4",2,"female","none",3,"car_other",38,"bank","rent",2,"unemployed",1,"yes","yes","No Risk"],
["greater_200",4,"prior_payments_delayed","furniture",3262,"less_100","1_to_4",2,"male","none",3,"savings_insurance",31,"none","free",1,"management_self-employed",1,"yes","yes","No Risk"],
["less_0",28,"outstanding_credit","business",2891,"100_to_500","4_to_7",4,"male","co-applicant",2,"savings_insurance",40,"none","own",1,"skilled",1,"yes","yes","Risk"],

["0_to_200",28,"credits_paid_to_date","education",1531,"less_100","4_to_7",2,"male","none",2,"car_other",28,"stores","own",1,"skilled",1,"yes","yes","Risk"],
["no_checking",41,"prior_payments_delayed","repairs",7507,"unknown","4_to_7",5,"male","co-applicant",5,"car_other",41,"none","own",2,"skilled",2,"none","yes","No Risk"],
["0_to_200",4,"prior_payments_delayed","vacation",250,"500_to_1000","4_to_7",2,"male","none",3,"savings_insurance",27,"none","own",1,"skilled",1,"none","yes","No Risk"]
]
}
```

## 上载反馈数据
{: #fmt-upld-fdbk-data-uploading}

您可以直接在 {{site.data.keyword.aios_short}} 用户界面中从 CSV 文件上载反馈数据。要上载 JSON 文件，可以使用 {{site.data.keyword.DSX}}。 

### 上载 CSV 文件
{: #fmt-upld-fdbk-data-upld-csv}

要上载 CSV 文件，请使用**添加反馈数据**按钮。

1. 从 {{site.data.keyword.aios_short}} 仪表板中，单击部署磁贴。
2. 从模型部署窗口中，单击**配置** ![显示部署配置按钮](images/configure-deployment-button.png) 图标。
3. 单击**添加反馈数据**按钮，选择包含反馈数据的 CSV 文件，然后单击**打开**。
4. 从下拉菜单中，单击字段分隔符，然后单击**选择**。

### 上载 JSON 文件
{: #fmt-upld-fdbk-data-upld-json}

1. 启动 {{site.data.keyword.DSX}} 并转至包含模型的项目。
2. 下载 JSON 文件。
1. 从 {{site.data.keyword.DSX}} 项目的**部署**选项卡中，单击 **model** 链接，单击**测试**选项卡，然后选择 JSON 输入图标。

    ![JSON 测试](images/json_test02.png)

1.  现在，打开所下载的 JSON 文件，并将内容复制到**测试**选项卡中的 JSON 字段。单击**预测**按钮以向模型发送训练载荷并对其进行评分。
