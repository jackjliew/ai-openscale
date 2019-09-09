---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-09"

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

# Formatting and uploading feedback data in {{site.data.keyword.aios_short}}
{: #fmt-upld-fdbk-data}

Feedback data is essential to maintain an unbiased model. You must upload feedback data to the {{site.data.keyword.aios_full}} service on a regular basis to ensure that your model takes into account up-to-date data that may indicate changes in the context of your predictive application.  With a feedback loop, the system learns continuously by monitoring the effectiveness of predictions and retraining when needed. Monitoring and using the resulting feedback are at the core of machine learning. The following information is meant to help you with formatting and uploading your feedback data.
(: shortdesc)

## Formatting feedback data
{: #fmt-upld-fdbk-data-fmt}

To read feedback data properly, it must be formatted properly. The  {{site.data.keyword.aios_short}} service accepts the following formats:

- CSV file formats, which can be uploaded by using the UI or the REST API
- JSON file formats, which can only be uploaded by using the REST API

These file formats are defined by a schema, `training_data_schema`, which is available in the subscription details. To view the  `training_data_schema`, run the following command by using the Python API:

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

To compare the training data schema to the feedback schema, you might want to view the feedback schema as well. To view the feedback schema, run the following command by using the Python API:

```
subscription.feedback_logging.print_table_schema()
```


### CSV format
{: #fmt-upld-fdbk-data-fmt-csv}

Typically for a CSV file you provide data in columns and rows with a row for column names.

No double quotation marks (") are needed when the column names are all uppercase, which makes them case-insensitive for Db2, however for other databases and in the instance where column names are mixed case, the case must match.
 
The feedback CSV file is expected to have all feature values, and the manually assigned target/label value. For example, the drug model training data contains feature values `AGE`, `SEX`, `BP`, `CHOLESTEROL`,`NA`,`K`, and the target/label value `DRUG`. The feedback CSV file needs to include values for those fields; an example would look like `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`. If a header is provided for the feedback CSV file, then field names are mapped using the header. Otherwise the field order **MUST** be exactly the same as in the training schema. For more information about training data, see [Why does {{site.data.keyword.aios_short}} need access to my training data?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) 

Please note that prediction types returned by your model, and the label/target column in your feedback data, must match.
{: note}

File sizes are currently limited to 8MB.
{: note}

If the file contains column names, columns do not necessarily have to match the table order, however, if the file has no column names, you must match the table order. It is possible to have columns that are not in the original training data. These columns are ignored during processing. The following sample shows a validly formatted CSV format file where double quotation marks (") are used for the column names:

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

### JSON format
{: #fmt-upld-fdbk-data-fmt-json}

The JSON format consists of a collection of objects with fields corresponding to column names. The following sample shows a complete, validly formatted JSON format file:


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

## Uploading feedback data
{: #fmt-upld-fdbk-data-uploading}

You can upload feedback data from a CSV file directly in the {{site.data.keyword.aios_short}} user interface. For uploading a JSON file, you can use {{site.data.keyword.DSX}}. 

### Uploading a CSV file
{: #fmt-upld-fdbk-data-upld-csv}

To upload a CSV file, use the **Add feedback data** button. To follow along with the following steps as part of the tutorial, open and copy the contents of the [`credit_feedback_data.csv`](https://raw.githubusercontent.com/watson-developer-cloud/doc-tutorial-downloads/master/ai-openscale/credit_feedback_data.csv){: external} file.

1. From the {{site.data.keyword.aios_short}} dashboard, click the deployment tile.
2. From the model deployment window, click **Configuration monitors** ![the deployment configuration button is shown](images/configure-deployment-button.png).
3. In the navigation pane, click **Quality**.
4. Click **Feedback** and then click the **Add feedback data** button.
5. Select the CSV file that contains the feedback data, and click **Open**. For the tutorial, select the `credit_feedback_data.csv` file you downloaded.

    File sizes are currently limited to 8 MB.
    {: note}

4. From the drop-down menu, click the field delimiter and click **Select**.

Adding the CSV file provides feedback data to your model.
### Uploading a JSON file
{: #fmt-upld-fdbk-data-upld-json}

1. Launch {{site.data.keyword.DSX}} and go to the project that contains the model.
2. Download the JSON file.
1. From the **Deployments** tab of your {{site.data.keyword.DSX}} project, click the **model** link, click the **Test** tab, and select the JSON input icon.

    ![JSON test](images/json_test02.png)

1.  Now, open the JSON file you downloaded, and copy the contents to the JSON field in the **Test** tab. Click the **Predict** button to send and score training payloads to your model.

### Viewing results
{: #fmt-upld-fdbk-view-results-after}

To check the result immediately, from the **Insights** page, select a deployment, click one of the **Quality** metrics, and then click **Check quality now**.
