---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Formattazione e caricamento dei dati di feedback in {{site.data.keyword.aios_short}}
{: #fmt-upld-fdbk-data}

I dati di feedback sono essenziali per gestire un modello senza distorsione. È necessario caricare i dati di feedback nel servizio {{site.data.keyword.aios_full}} regolarmente per garantire che il modello prenda in considerazione i dati aggiornati che possono indicare modifiche nel contesto dell'applicazione predittiva.  Con un loop di feedback, il sistema impara continuamente, monitorando l'efficacia delle previsioni e rieseguendo il training quando necessario. Il monitoraggio e l'utilizzo del feedback risultante sono alla base del machine learning. Le seguenti informazioni sono intese a guidare l'utente nella formattazione e nel caricamento dei dati di feedback.
(: shortdesc)

## Formattazione dei dati di feedback
{: #fmt-upld-fdbk-data-fmt}

Per leggere correttamente i dati di feedback, devono essere formattati in modo appropriato. Il servizio {{site.data.keyword.aios_short}} accetta i seguenti formati:

- Formati file CSV, che è possibile caricare utilizzando la IU o l'API REST
- Formati file JSON, che possono essere caricati utilizzando solo l'API REST

Questi formati di file sono definiti da uno schema, `schema_dati_training`, disponibile nei dettagli di sottoscrizione. Per visualizzare lo `schema_dati_training`, eseguire il seguente comando utilizzando l'API Python:

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

Per confrontare lo schema dei dati di training con lo schema di feedback, è possibile voler visualizzare anche lo schema di feedback. Per visualizzare lo schema di feedback, eseguire il seguente comando utilizzando l'API Python:

```
subscription.feedback_logging.print_table_schema()
```


### Formato CSV
{: #fmt-upld-fdbk-data-fmt-csv}

Generalmente, per un file CSV si forniscono i dati in colonne e righe con una riga per i nomi colonna.

Non sono richieste le virgolette (") quando i nomi colonna sono tutti in maiuscolo, ciò li rende non sensibili al maiuscolo/minuscolo per Db2, tuttavia per altri database e nel caso in cui i caratteri dei nomi sono misti, il maiuscolo/minuscolo deve corrispondere.
 
È previsto che il file CSV di feedback abbia tutti i valori funzione e il valore destinazione/etichetta assegnato manualmente. Ad esempio, i dati di training del modello Drug contengono i valori funzione `AGE`, `SEX`, `BP`, `CHOLESTEROL`,`NA`,`K` e il valore destinazione/etichetta `DRUG`. Il file CSV di feedback deve includere i valori per quei campi; un esempio potrebbe assomigli a `[43, M, HIGH, NORMAL, 0.6345, 1.4587, DrugX]`. Se viene fornita un'intestazione per il file CSV di feedback, i nomi di campo vengono associati utilizzando l'intestazione. Altrimenti l'ordine dei campi **DEVE** essere esattamente uguale a quello dello schema di training. Per ulteriori informazioni sui dati di training, consultare [Perché {{site.data.keyword.aios_short}} ha bisogno di accedere ai miei dati di training?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata) 

Si noti che i tipi di previsione restituiti dal modello, e la colonna etichetta/destinazione nei dati di feedback, devono corrispondere.
{: note}

La dimensione dei file è attualmente limitate a 8MB.
{: note}

Se il file contiene nomi colonna, le colonne non devono necessariamente corrispondere all'ordine della tabella, tuttavia se il file non ha nomi colonna, è necessario mettere in corrispondenza con l'ordine della tabella. È possibile avere colonne che non sono nei dati di training originali. Tali colonne vengono ignorate durante l'elaborazione. Il seguente esempio mostra un file in formato CSV correttamente formattato dove vengono utilizzate le virgolette (") per i nomi di colonna:

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

### Formato JSON
{: #fmt-upld-fdbk-data-fmt-json}

Il formato JSON consiste di una raccolta di ogegtti con campi corrispondenti ai nomi colonna. Il seguente esempio mostra un file in formato JSON formattato correttamente, completo:


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

## Caricamento dei dati di feedback
{: #fmt-upld-fdbk-data-uploading}

È possibile caricare i dati di feedback da un file CSV direttamente nell'interfaccia utente {{site.data.keyword.aios_short}}. Per il caricamento di un file JSON, è possibile utilizzare {{site.data.keyword.DSX}}. 

### Caricamento di un file CSV
{: #fmt-upld-fdbk-data-upld-csv}

Per caricare un file CSV, utilizzare il pulsante **Aggiungi dati di feedback**.

1. Dal dashboard {{site.data.keyword.aios_short}}, fare clic sul riquadro di distribuzione.
2. Dalla finestra di distribuzione del modello, fare clic sull'icona **Configurazione**![viene visualizzato il pulsante di configurazione della distribuzione](images/configure-deployment-button.png).
3. Fare clic sul pulsante **Aggiungi dati di feedback**, selezionare il file CSV che contiene i dati di feedback e fare clic su **Apri**.
4. Dal menu a discesa, fare clic sul delimitatore campo e su **Seleziona**.

### Caricamento di un file JSON
{: #fmt-upld-fdbk-data-upld-json}

1. Avviare {{site.data.keyword.DSX}} e andare al progetto che contiene il modello.
2. Scaricare il file JSON.
1. Dalla scheda **Distribuzioni** del progetto {{site.data.keyword.DSX}}, fare clic sul link **model**, fare clic sulla scheda **Verifica** e selezionare l'icona di input JSON.

    ![Verifica JSON](images/json_test02.png)

1.  Ora, aprire il file JSON scaricato e copiare il contenuto nel campo JSON nella scheda **Verifica**. Fare clic sul pulsante **Previsione** per inviare e assegnare un punteggio ai payload di training al modello.
