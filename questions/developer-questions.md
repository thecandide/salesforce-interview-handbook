# Salesforce Develop Questions

Pull requests for suggestions and corrections are welcome!

Fundamentals
* [What are governor limits? Why are they important?](#what-are-governor-limits-why-are-they-important)
* [What are the Bulkification best practices?](#what-are-the-bulkification-best-practices)
* [What are the key automation tools in Salesforce? How do you know when to use which?](#what-are-the-key-automation-tools-in-Salesforce-how-do-you-know-when-to-use-which)
* [What is the difference between force.com and salesforce.com?](#what-is-the-difference-between-force.com-and-salesforce.com)

Sharing & Security
* [What are the different ways we can share a record?](#what-are-the-different-ways-we-can-share-a-record)
* [What are sharing settings? Why are they important?](#what-are-sharing-settings-why-are-they-important)
* [What is Apex Managed Sharing?](#what-is-apex-managed-sharing)
* [How many ways can we share a record?](#how-many-ways-can-we-share-a-record)


Behavioral
* [What are your 3 favourite Salesforce blogs?](#what-are-your-3-favourite-Salesforce-blogs)
* [Do you attend Salesforce developer community meetings?](#do-you-attend-Salesforce-developer-community-meetings)
* [What do you do when you are stuck when you code?](#what-do-you-do-when-you-are-stuck-when-you-code)
* [How many reputation points do you have on salesforce StackEchange?](#how-many-reputation-points-do-you-have-on-salesforce-stackExchange)
* [Would you say you are passionate about Salesforce? If so why?](#would-you-say-you-are-passionate-about-salesforce-if-so-why)
* [Have you ever contributed to Salesforce's Ideas? If you could make any idea come true, what would it be?](#have-you-ever-contributed-to-salesforces-ideas-if-you-could-make-any-idea-come-true-what-would-it-be)
* [Where do you see yourself in 3 years?](#where-do-you-see-yourself-in-3-years)
* [Do you enjoy being a Salesforce developer? Why?](#do-you-enjoy-being-a-salesforce-developer-why)

SOQL & DML
* [What are the default indexed fields in Salesforce?](#what-are-the-default-indexed-fields-in-Salesforce)
* [What is difference insert() and database.insert()?](#what-is-difference-insert-and-database.insert)

Data Modelling & Data Management
* [What Are The Types of SOQL Statements in SalesForce?](#what-are-the-types-of-soql-statements-in-salesforce)
* [When one wants to pass the collection to the query instead of passing one value which keyword helps us?](#when-one-wants-to-pass-the-collection-to-the-query-instead-of-passing-one-value-which-keyword-helps-us)
* [What is Future Annotation(@Future)?](#what-is-future-annotation-future)
* [What is Data Skew?](#what-is-data-skew)
* [Explain skinny table. What are the considerations for Skinny Table?](#explain-skinny-table-what-are-the-considerations-for-skinny-table)
* [Which fields are automatically Indexed in Salesforce?](#what-are-the-default-indexed-fields-in-Salesforce)
* [Which fields are excluded from a custom index?](#which-fields-are-excluded-from-a-custom-index)

Logic & Process Automation 
* [What are the types of custom settings in Salesforce? What is the advantage of using custom settings?](#what-are-the-types-of-custom-settings-in-salesforce-what-is-the-advantage-of-using-custom-settings)
* [What are custom labels in Salesforce? What is the character limit of custom label?](#what-are-custom-labels-in-salesforce-what-is-the-character-limit-of-custom-label)
* [What are deterministic formula fields in Salesforce?](#what-are-deterministic-formula-fields-in-salesforce)

Apex
* [Why do we need to write test classes? How to identify if a class is a test class?](#)
* [Why do we use start test & stop test annotations?](#)
* [Why do we need to write test classes? How to identify if a class is a test class?](#)
* [What are the best practices for writing test classes?](#)
* [Name 3 governor limits you know? Why are they important? How do you resolve when you see such errors?](#)
* [What are the different types of collections in Apex? What are maps in Apex?](#w)
* [What is the use of “@future” annotation?](#)
* [What are the different methods of batch Apex class?](#)
* [What is Trigger.new?](#)
* [What is the difference between SOQL and SOSL?](#what)
* [What is the difference between public and global class in Apex?](#wha)
* [What are the two options for when Apex Triggers can run?](#whats)
* [What is a use case for sharing rules?](#what-are-some-of-the)
* [Explain the use of an Outbound Message?](#what)
* [What is Trigger.new?](#what)
* [What is the Save Order of Execution? Why is it important?](#what)
* [What is a wrapper class? Give one use case where you would use a wrapper class.](#what)
* [Explain various methods of batch Apex class?](#what)
* [What is Apex Email Service?](#)
* [Describe the 3 qualities of Apex that make it powerful?](#)
* [What is Map Class in Apex Salesforce?](#)
* [What is Batch Apex in Salesforce?](#)
* [What is Apex Scheduler?](#)
* [What is the Apex Trigger in Salesforce?](#)
* [What is an Apex transactions?](#)
* [What are static resources?](#)
* [What is the difference between public and global classes in Apex?](#h)
* [Why use Batch Apex instead of Normal Apex?](#have-you-ever-used-a-grid-system-and-if-so-what-do-you-prefer)
* [What the difference between isNull and isBlank?](#have-you-ever-used-a-grid-system-and-if-so-what-do-you-prefer)

Debug & Deployment Tools
* [What are the different ways of deployment in Salesforce?](#what-are-the-different-ways-of-deployment-in-salesforce)
* [Why do we need to write test classes? How to identify if a class is a test class?](#why-do-we-need-to-write-test-classes-how-to-identify-if-a-class-is-a-test-class)


Scenario Based Questions
* [ What does it indicate if an error state this “list has no rows for assignment”?](#what-does-it-indicate-if-an-error-state-this-list-has-no-rows-for-assignment)


### What are the Bulkification best practices?

- Nested loops must be boycotted.
- Soql queries inside loops must be avoided.
- Use simple FOR loop instead of FOR each for better efficiency.
	Ex: 
	List<String> Accountkeys = new List<String>();
	for(integer i=0; i < Accountkeys.size(); ++i) { system.debug(Accountkeys[i])} <== Consumes lesser time
	for(String key : Accountkeys){ system.debug(key)} <== consumes more time
- Use collections like map to store data locally, so that you can get rid of expensive database calls.
- Always keep one trigger per object. No matter how complex one trigger becomes but multiple trigger misbehaves during bulk execution. You can use helper methods to reduce the complexity of the trigger also.
- Use batch class as much as you can during bulk operations as they have been designed to handle bulk easily.
- Keep track of limits by using Limits class to avoid hitting governor limits.
- Future methods are very helpful when you have to update a large set of data. You can continue with your synchronous transaction and save time for updation by asking future method to update records asynchronously.

[[↑] Back to top](#css-questions)

### What are the key automation tools in Salesforce? How do you know when to use which?

- In salesforce, Process builder , Workflow, Flow builder and approval process are some key tools for automation.
- All these tools have separate significance to perform various business processes in salesforce.
- When you have a requirement of processing multiple statements together, process builder or flow builder should be your choice.
- When you want some action to be performed automatically on basis of time, you should refrain from using approval process.
- If you want an activity to be done based on user action, Flow builder is an ideal choice.
- If calling an apex class is a necessity, Process builder can be used.
- For Sending outbound messages, workflows have been recommended.
 So based on the various needs various automation can be utilized. Please have a look at below table which describes the uses of each automation in a better way.
 
<img src="/assets/Automated_features.PNG">

[[↑] Back to top](#css-questions)

### What are the different ways we can share a record?
We can share records using:
1. Roles
1. orgwidedefaults
1. Apex Sharing
1. Manual sharing
1. Sharing rules.

[[↑] Back to top](#css-questions)

### What are sharing settings? Why are they important?

- The whole concept of access control can be visualized as 3 gates before you reach the treasury box (Speaking in layman terms)
- Like you have to cross all the gates to reach the treasure, the same way you have to cross path with 3 levels of configuration to actually achieve a successful access control on data. You can consider the 3 gates as metadata accesses to achieve the access on actual data. These gates are object setting, field settings and sharing settings which relates to object, field and the record respectively. Once you have object and field level permissions, you can choose to have record level permissions using sharing settings.
- Sharing settings can be achieved through Orgwidedefaults, Sharing rules or Apex sharing.
- For understanding its importantance, lets take a scenario: A multinational company does their business in various regions. Director of Finland watches the business in Finland and Director of India watches it in India. If director of india starts to see the business done by company in Finland too with total figures of India then it will becomes cumbersome for him to do analysis for a specific region. Hence, allowing the respective directors to see data of their region only may lead to increased analysis and sales. This simple scenario can be achieved using OWDs and sharing rules.

[[↑] Back to top](#css-questions)

### What is Apex Managed Sharing?

Apex Sharing is a ability provided to force.com developers to explicitly fullfill the requirement of record sharing of an application or a product programatically. If you want to built an app which shares records based on some criteria due to an event occurance, then nothing other than apex sharing can help you.
For example, AccountShare is the sharing object for the Account object, ContactShare is the sharing object for the Contact object, MyCustomObject will be named as MyCustomObject__Share.

[[↑] Back to top](#css-questions)

### How many ways can we share a record?
There are 5 ways to share a record:
1. Roles
1. OWDs
1. Apex Sharing
1. Manual sharing
1. Sharing rules.

[[↑] Back to top](#css-questions)

### What are your 3 favourite Salesforce blogs?

My personal favourites Salesforce bloggers are:
1. http://www.asagarwal.com         >>> lots of fantastic step-by-step guides
1. http://www.jitendrazaa.com/blog/ >>> fantastic articles on different topics, i.e. best chrome extensions for Salesforce
1. http://sfdcmonkey.com/	    >>> brings together best articles on everything related to Lightning

[[↑] Back to top](#css-questions)

### Do you attend Salesforce developer community meetings?

`TextBook Definition:`
Yes I do attend developer community meetings every single time. These meetings boosts myself in terms of knowledge gains and public relations. I have even got chance to speak in the community and share my knowledge. I have been rewarded with more than 10 rewards by community which motivates myself a lot.

`Street Definition:`
You know, Salesforce developer community meetings are my favourite. I make new friends every time. I learn and share in these meetings. Moreover, the food offered in the break is awesome. I am always excited for Q&A section where i had already grabbed tens of gifts and planning to pull more.

[[↑] Back to top](#css-questions)

### What do you do when you are stuck when you code?

`TextBook Definition:`
There are certain times when i get stuck while coding. In such case, I generally do some r&d on the internet crawling through many blogs and vlogs searching for solution. I try to find my doubts in developer forums or even post a question when no similiar question have been found. Once i find a solution, i apply it or in case no solution is available then i find a workaround. My first step generally is to google the exact error and know the root cause. Before moving to a workaround, i always consult a senior developer as experience is the key to solution.
Ex: I faced an error called "Mixed Dml exception" someday. I searched for the error on the internet for knowing the root cause. After reading few blogs, i came to know that it happens due to Dml of setup and non setup objects in the same transaction. Then i searched for the ways to separate that transaction. I found a clue Future methods. Then i searched for future methods and its syntax and embedded the solution.

`Street Definition:`
The first and foremost thing to fight to such a situation is not to loose faith in yourself. The best solution can be generated by you and you only. With that in mind, start googling the exact error or exception. Be brave, search for more blogs if the root cause is still hazy. There are leads or others developers to help you but you have to try to solve it on your own within a specified timeframe. If it's too much time consumed without even a clue, consult the lead immediately. You have already won the half way if you know the root cause. Because once you know the reason, you may have various way to solve it. Once sorted, say thanks to google and god!

[[↑] Back to top](#css-questions)

### How many reputation points do you have on salesforce StackExchange?

`TextBook Definition:`
On StackExchange i just have 100 points currently. Reputation points on Stackexchange came on to my priority list a bit late but yes it is there in my bucket. Moreover, i am targetting to reach 1000 points very soon in a month or so.

`Street Definition:`
I use stackexchange relatively very less. Whenever i am stuck technically, i search for solutions on it and apart from this i am very less active. But recently i have started answering the questions for which i am pretty sure and you won't believe it gives me immense pleasure to help the community and earn a label in return. I compete with friends nowadays and excel myself. I have 100 points now which will be 1000 soon.

[[↑] Back to top](#css-questions)

### Would you say you are passionate about Salesforce? If so why?

`TextBook Definition:`
I started working on salesforce due to a project requirement. The UI and funtionalities in salesforce attracted me towards it. When i came to know about solid functionality like sharing settings, I was absolutely amazed because when i compare it will other technologies or CRMs, it is really time consuming job to make such a funtionality whereas in salesforce you are getting it prebuilt. Hence it increased me interest. I started believing in salesforce when saw its thrice in a year upgrade process and most probably the dreamforce. Even writting code in apex and lightning are pretty straightforward and there are huge bunch of blogs and a wide community always ready to help. Finally it became my passion when i successfully deployed one project with full support from salesforce partners, salesforce community and the salesforce case support. Moreover, it also provided cetified developers and admins, hence finally with passion i selected it as my career.

`Street Definition:`
Frankly speaking, i came into salesforce due to high market demand and less developers available. Obviously a good pay was my first reason, but when i started exploring this CRM in depth i had no clue what i was looking it. At first it looked really difficult, so mamy thing so many functionality at one place but once i got a command using trailhead and the blogs, i was unstoppable. Sharing settings, profile and users, all other setup stuffs were mind bending initially but i grasped them and now i feel that there can be no better CRM to do this. Writting code in salesforce seems very much easy to me then any other technologies due to the really good supportive development environment. I started loving salesforce when i realized i am growing day by day in terms of knowledge, market upgradation, working with better clients and infrastructure and finally in payscale. Even such rapid growth of salesforce motivated me to stay connected to the community and love what you do. Hence salesforce became my passion and career both.

[[↑] Back to top](#css-questions)

### Have you ever contributed to Salesforce's Ideas? If you could make any idea come true, what would it be?

`TextBook Definition:`
Yes, i always wished the Lookup rollup functionality should be a part of salesforce itself due to the daily demands. I hope salesforce may find it useful. By the way, we can't add rollup summary fields on lookup relationship and i wished if that is possible too with restrictions.

`Street Definition:`
I have already contribited the idea of Lookup rollup and asked the community to vote it. Tht thing is - in the intial stage of the project you sometimes are not sure what relation should be taken up, consider you choose lookup at that time, further at the later part of the project you got a functionlity to count child records and that becomes a mess at that time. You may have to write custom code for that. I believe that should already be there and recommend salesforce to add it. But again they are the better judge.

[[↑] Back to top](#css-questions)

### Where do you see yourself in 3 years?

`TextBook Definition:`
Currently i am a developer with good coding and learning skills but i know that not enough. I have to rise to a technical lead position next coming years and despite of coding, i have to focus on becoming a good observer, orator, multi-tasker and a quick issue discoverer. With all these, new platform changes should also be grasped. I also have to serve the company by becoming their crucial asset earning handful of appreciations for myself. So in conclusion i want to be an expert of this domain, lead the projects and take the managerial responsibilities.

`Street Definition:`
In next 3 years, i want to learn every aspect of salesforce development. Either it is lightning components or lightning web components, i want to be fully expert on them with a live project hands on. I am looking for a designation step up with full confidence in handling a project smoothly. I have already handled modules in the past and i feel i am ready for the whole project itself. Although, every four month salesforce produces something new, it would also make myself a better developer day by day. Further, buying a car, marriage etc are also the part of my life in next 3 years. Yah, One thing i forgot is the World tour, hope to save much to complete a world tour soon.

[[↑] Back to top](#css-questions)

### Do you enjoy being a Salesforce developer? Why?

`TextBook Definition:`
First things, you are working with a world dominating technology and you should be happy about it. This is an innovative platform which does innovations and ask you to be part of them. You may always find some traning guides and issue resolution steps somewhere. Readily available code repositories, appexchange products and function librabaries are always available to skip to start from scratch. The compiler and interpreter of the apex engine are seriously appreciated which helps you rectify your code in minutes. Further, the community trains and certify you also. So all in all salesforce development is the one i love.

`Street Definition:`
I am glad being one. Being salesforce developer is really an exciting job. It is for the people who seek adventure and never wish to settle down. The new generation is of that kind which wants to keep learning daily and salesforce is always ready to teach you. It keeps on upgrading the technology as per modern needs and forces its community to learn to catch up the market. It shows trust on you by certifying you and ensuring the community that he is worth it. You learn from trailhead, you apply it in real time, you search in community to help and you deliver it. There is no way you will be stuck, someone will always be there to help you. That's why i like being a exciting salesforce developer.

[[↑] Back to top](#css-questions)


### What are governor limits? Why are they important?

Governor limits are runtime limits enforced by the Apex runtime engine to ensure that code does not monopolizes the resources which have been shared by various customers and organizations. These limits ensure the efficient processing of resources on the Force.com multitenant platform.


[[↑] Back to top](#css-questions)

### What is the difference between force.com and salesforce.com?

- Salesforce.com is SAAS and force.com is PAAS.
- All the prebuilt products like sales or service, leads, reports, tabs etc are a part of salesforce.com and the possible customization products like visualforce page, classes, triggers, components etc are a part of force.com.
- Licenses for salesforce.com are pretty expensive than force.com's license.
- Salesforce.com is a leading CRM which have been built for targetting customers and social objectives whereas force.com helps delivering world class customized apps within short period of time.
- Salesforce.com focuses more on prebuilt functionality to complete stuffs by points and clicks whereas force.com uses programming or markup languages to build a product or output which is not offered as a part of salesforce CRM.
- Salesforce.com is a product built on the top of force.com platform.

[[↑] Back to top](#css-questions)

### What are the default indexed fields in Salesforce?

`Textbook Definition:`
There are certain types of index fields in salesforce as stated below.
- Primary keys (Id, Name, and Owner fields).
- Foreign keys (Relationship fields like lookup or master detail).
- Dates fields (such as LastModifiedDate,createddate).

`Street Definition:`
Most of the system fields which acts as the key in their particular table are indexed fields. Like Account ID is an primary field of account table so it have been indexed. OwnerId on account is also an indexed field as it is a foreign key in account table representing users table. Indexing a fields makes database operation really fast so i many times use an external id field also for many purposes, but that is not default, rather a custom solution.

[[↑] Back to top](#css-questions)

### What is difference insert() and database.insert()?

`Textbook Definition:`
- DML Insert is known as a Dml statement whereas Database.insert() is a method derived from database class.
- Database insert is parameterized to support partial insert which is not possible in DML insert.
- DML insert doesn't support rollback which is a useful feature of Database.insert().
- DML insert doesn't return error or success records for further processing whereas Database.insert does.

`Street Definition:`
- For a bulk operation, if you wish to cancel the operation even if a single record gets errored out of bulk then you should use Insert() or if you wish you partially insert records and separate the failed once then you should use Database.insert().
- For exception handling, Database.insert() returns database.saveResult class so you can automatically create your own failed records object and process the inserted one. But if you want to rerun the operation then use Try catch block with insert() as per your needs.
- Using Database.insert() you can rollback very easily through parameters. However, rolling back using insert() is bit indirect. You can use try catch block and rollup in catch statement using Databse.rollback() method.
Example:
If we are inserting 200 records in an object, Where 5 records are prone to error and remaining others records are good.
In DML statement (Insert) all the 200 records will be failed, because if one record is incorrect or error means all other remaining records will not be inserted. It will throw error.
In Database.insert 195 records will be inserted, remaining 5 records will be failed.

[[↑] Back to top](#css-questions)

### What Are The Types of SOQL Statements in SalesForce?

`Textbook Definition:`
There are two types of SOQl statements Dynamic and Static. You can use either of them as per your needs.
Example-
String accountname = 'Salesforce Chef';
[select id from account where name=:accountname] ==> Static
String query = 'select id from account where name=\'' + accountname + '\''; ==> Dynamic

[[↑] Back to top](#css-questions)

### When one wants to pass the collection to the query instead of passing one value which keyword helps us?

`Textbook Definition:`
IN keyword is used to pass a collection to the query.
Example-
List<String> AccountNames =  new List<String>('Youtube','Microsoft');
[select id from account where name IN :AccountNames]

[[↑] Back to top](#css-questions)

### What is Future Annotation(@Future)?

`Textbook Definition:`
Future annotation identifies the method to run in separate thread asynchronously whenever the resources are available.

`Street Definition:`
Future annotation is used to mark a method as future method and future methods have the capability to run apart of the current context so that performance of the current operation can be enhanced by ensuring less chances of hitting a governor limit. Future methods run whether system have available resources so it will never hamper other processes.

[[↑] Back to top](#css-questions)

### What is Data Skew?

`Textbook Definition:`
When a parent have huge number of child records related to it through special relationships, then an imbalance occurs in the system which directly impacts the performance of the org. This situation is called as Data Skew. This huge number represents 10,000 or more.

`Street Definition:`
When a record or an account have more than 10,000 childs associated with it, we call this situation as Data Skew.

[[↑] Back to top](#css-questions)

### Explain skinny table. What are the considerations for Skinny Table?

`Textbook Definition:`
Skinny tables generally contain frequently used fields and avoid joins. They tend to improve the performance of many read-only operations. Skinny tables are kept in sync with their source tables when the source tables are modified.
Considerations:
-Skinny tables can contain a maximum of 100 columns.
-Skinny tables can’t contain fields from other objects.
-For Full sandboxes: Skinny tables are copied to your Full sandbox orgs.

`Street Definition:`
Consider the skinny table as the index of the book. How easy it is to move to the topic of a heavy book you want to read by refering its page number from the index? and imagine the situation when the index of the book had been torn and you need to reach the particular topic, very disgusting! Similarly, when there are more than 2 million records in the org for a single object and you want to query one it will be a havok as you may face performance issues. To get rid of that, contact salesforce customer support and ask them to create a skinny table to the particular object. These skinny tables will act as an index in the database and may speed up many operations. These skinny tables are invisible to us and may be automatically used whereever applicable. Simple meaning of creating a skinny table is to make a field indexed and add it to a separate table. Every time you want to make a field indexed you need to contact salesforce support and ask the particular field to be added into the skinny table. With that benefit, salesforce have also placed some restricted on skinny table, please read the textbook definition for these restrictions or considerations.

[[↑] Back to top](#css-questions)

### Which fields are excluded from a custom index?

`Textbook definition`
Various custom fields like multi-select picklists, text area (long), text area (rich), non-deterministic formula fields, and encrypted text field are excluded from the custom index.

`Street Definition:`
The fields which are either encrypted or designed to carry huge data like comments or description are excluded from custom index. Index is a key which takes you to main data so there is no point of storing huge data in the index rather your index should point to huge data.

[[↑] Back to top](#css-questions)

### What are the types of custom settings in Salesforce? What is the advantage of using custom settings?

`Textbook Definition:`
There are two types of custom settings Heirarchy and List. The custom settings are basically stored in application cache memory and hence you don't need expensive DML calls to retrieve them. Even they are faster to access.

`Street Definition:`
Types of custom settings are already known to you. Since cache memory have better read write speeds than hard drives, custom settings are stored in this memory in order to retrieve data urgently and without any DML calls. So store your frequently used data in custom setting to stay away from governor limit hit.

[[↑] Back to top](#css-questions)

### What are custom labels in Salesforce? What is the character limit of custom label?

`Textbook Definition:`
Custom labels are custom multilingual text values that can be accessed from Apex classes or Visualforce pages. They are generally used to develop custom multilingual applications. Each custom label has a limit of 1000 characters.

`Street Definition:`
Consider you are a end user and you downloaded an app exchange product. You liked the product and want to switch to your native lamguage instead of english. How can developers achieve this? They can't write various langugues on the visualforce page or component, hence they use custom labels which change their language dynamically based on user language selection.

[[↑] Back to top](#css-questions)

### What are deterministic formula fields in Salesforce?

`Textbook Definition:`
The Formula fields whose value will be static and might not vary over time when a transaction updates a related entity, are called as deterministic formula fields. For being deterministic, value of formula fields should not be calculated on fly.

`Street Definition:`
You can make your formula fields deterministic by using only current object fields in the formula (no cross object formulas), not making dependency on current date and no reference to special fields.
Example:
Consider you have two fields on account: Company name and Account number.
You want to create a key which concates both the fields, creating formula will be a wisely decision and such a field is deterministic.

[[↑] Back to top](#css-questions)

### What are the different ways of deployment in Salesforce?

`Textbook Definition:`
Change Sets - native salesforce solution
Eclipse with Force.com IDE - widely used IDE
Ant migration tool - java based utility
Salesforce Package - managed or unmanged package

[[↑] Back to top](#css-questions)

### Why do we need to write test classes? How to identify if a class is a test class?

`Textbook Definition:`
Salesforce strongly recommends using a test-driven development process which occurs at the same time as code development that means only the quality code should be deployed to production. For checking the quality of code, salesforce performs unit testing at their end while deployment. This unit testing is achieved using test classes and hence without test classes there can be no deployment in salesforce. Such a test class should cover minimum 75% test cases and is identified by @isTest annontation over the class declaration.

[[↑] Back to top](#css-questions)

### What does it indicate if an error state this “list has no rows for assignment”?

`Textbook Explanation:`
This is System.Query Exception. This error means that the query which you fired returned no records from the database so the program can't assign anything to the variable.
Example:
Account acc = [select id from account where name='Salesforce Chef'];
Consider the above query, if the there is no record in database with the name "Salesforce Chef" then the “list has no rows for assignment” error will occur saying "no records were found to assign data to acc".

[[↑] Back to top](#css-questions)

### What ar
e the advantages/disadvantages of using CSS preprocessors?

**Advantages:**

* CSS is made more maintainable.
* Easy to write nested selectors.
* Variables for consistent theming. Can share theme files across different projects.
* Mixins to generate repeated CSS.
* Sass features like loops, lists, and maps can make configuration easier and less verbose.
* Splitting your code into multiple files. CSS files can be split up too but doing so will require an HTTP request to download each CSS file.

**Disadvantages:**

* Requires tools for preprocessing. Re-compilation time can be slow.
* Not writing currently and potentially usable CSS. For example, by using something like [postcss-loader](https://github.com/postcss/postcss-loader) with [webpack](https://webpack.js.org/), you can write potentially future-compatible CSS, allowing you to use things like CSS variables instead of Sass variables. Thus, you're learning new skills that could pay off if/when they become standardized.

[[↑] Back to top](#css-questions)

### Describe what you like and dislike about the CSS preprocessors you have used.

**Likes:**

* Mostly the advantages mentioned above.
* Less is written in JavaScript, which plays well with Node.

**Dislikes:**

* I use Sass via `node-sass`, which is a binding for LibSass written in C++. I have to frequently recompile it when switching between node versions.
* In Less, variable names are prefixed with `@`, which can be confused with native CSS keywords like `@media`, `@import` and `@font-face` rule.

[[↑] Back to top](#css-questions)

### How would you implement a web design comp that uses non-standard fonts?

Use `@font-face` and define `font-family` for different `font-weight`s.

[[↑] Back to top](#css-questions)

### Explain how a browser determines what elements match a CSS selector.

This part is related to the above about [writing efficient CSS](#what-are-some-of-the-gotchas-for-writing-efficient-css). Browsers match selectors from rightmost (key selector) to left. Browsers filter out elements in the DOM according to the key selector and traverse up its parent elements to determine matches. The shorter the length of the selector chain, the faster the browser can determine if that element matches the selector.

For example with this selector `p span`, browsers firstly find all the `<span>` elements and traverse up its parent all the way up to the root to find the `<p>` element. For a particular `<span>`, as soon as it finds a `<p>`, it knows that the `<span>` matches and can stop its matching.

###### References

* https://stackoverflow.com/questions/5797014/why-do-browsers-match-css-selectors-from-right-to-left

[[↑] Back to top](#css-questions)

### Describe pseudo-elements and discuss what they are used for.

A CSS pseudo-element is a keyword added to a selector that lets you style a specific part of the selected element(s). They can be used for decoration (`:first-line`, `:first-letter`) or adding elements to the markup (combined with `content: ...`) without having to modify the markup (`:before`, `:after`).

* `:first-line` and `:first-letter` can be used to decorate text.
* Used in the `.clearfix` hack as shown above to add a zero-space element with `clear: both`.
* Triangular arrows in tooltips use `:before` and `:after`. Encourages separation of concerns because the triangle is considered part of styling and not really the DOM. It's not really possible to draw a triangle with just CSS styles without using an additional HTML element.

###### References

* https://css-tricks.com/almanac/selectors/a/after-and-before/

[[↑] Back to top](#css-questions)

### Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.

The CSS box model describes the rectangular boxes that are generated for elements in the document tree and laid out according to the visual formatting model. Each box has a content area (e.g. text, an image, etc.) and optional surrounding `padding`, `border`, and `margin` areas.

The CSS box model is responsible for calculating:

* How much space a block element takes up.
* Whether or not borders and/or margins overlap, or collapse.
* A box's dimensions.

The box model has the following rules:

* The dimensions of a block element are calculated by `width`, `height`, `padding`, `border`s, and `margin`s.
* If no `height` is specified, a block element will be as high as the content it contains, plus `padding` (unless there are floats, for which see below).
* If no `width` is specified, a non-floated block element will expand to fit the width of its parent minus `padding`.
* The `height` of an element is calculated by the content's `height`.
* The `width` of an element is calculated by the content's `width`.
* By default, `padding`s and `border`s are not part of the `width` and `height` of an element.

###### References

* https://www.smashingmagazine.com/2010/06/the-principles-of-cross-browser-css-coding/#understand-the-css-box-model

[[↑] Back to top](#css-questions)

### What does `* { box-sizing: border-box; }` do? What are its advantages?

* By default, elements have `box-sizing: content-box` applied, and only the content size is being accounted for.
* `box-sizing: border-box` changes how the `width` and `height` of elements are being calculated, `border` and `padding` are also being included in the calculation.
* The `height` of an element is now calculated by the content's `height` + vertical `padding` + vertical `border` width.
* The `width` of an element is now calculated by the content's `width` + horizontal `padding` + horizontal `border` width.
* Taking into account `padding`s and `border`s as part of our box model resonates better with how designers actually imagine content in grids.

###### References

* https://www.paulirish.com/2012/box-sizing-border-box-ftw/

[[↑] Back to top](#css-questions)

### What is the CSS `display` property and can you give a few examples of its use?

* `none`, `block`, `inline`, `inline-block`, `table`, `table-row`, `table-cell`, `list-item`.

TODO

[[↑] Back to top](#css-questions)

### What's the difference between `inline` and `inline-block`?

I shall throw in a comparison with `block` for good measure.

|                                      | `block`                                                                                     | `inline-block`                                                      | `inline`                                                                                                                                                                                                             |
| ------------------------------------ | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Size                                 | Fills up the width of its parent container.                                                 | Depends on content.                                                 | Depends on content.                                                                                                                                                                                                  |
| Positioning                          | Start on a new line and tolerates no HTML elements next to it (except when you add `float`) | Flows along with other content and allows other elements beside it. | Flows along with other content and allows other elements beside it.                                                                                                                                                  |
| Can specify `width` and `height`     | Yes                                                                                         | Yes                                                                 | No. Will ignore if being set.                                                                                                                                                                                        |
| Can be aligned with `vertical-align` | No                                                                                          | Yes                                                                 | Yes                                                                                                                                                                                                                  |
| Margins and paddings                 | All sides respected.                                                                        | All sides respected.                                                | Only horizontal sides respected. Vertical sides, if specified, do not affect layout. Vertical space it takes up depends on `line-height`, even though the `border` and `padding` appear visually around the content. |
| Float                                | -                                                                                           | -                                                                   | Becomes like a `block` element where you can set vertical margins and paddings.                                                                                                                                      |

[[↑] Back to top](#css-questions)

### What's the difference between a `relative`, `fixed`, `absolute` and `static`ally positioned element?

A positioned element is an element whose computed `position` property is either `relative`, `absolute`, `fixed` or `sticky`.

* `static` - The default position; the element will flow into the page as it normally would. The `top`, `right`, `bottom`, `left` and `z-index` properties do not apply.
* `relative` - The element's position is adjusted relative to itself, without changing layout (and thus leaving a gap for the element where it would have been had it not been positioned).
* `absolute` - The element is removed from the flow of the page and positioned at a specified position relative to its closest positioned ancestor if any, or otherwise relative to the initial containing block. Absolutely positioned boxes can have margins, and they do not collapse with any other margins. These elements do not affect the position of other elements.
* `fixed` - The element is removed from the flow of the page and positioned at a specified position relative to the viewport and doesn't move when scrolled.
* `sticky` - Sticky positioning is a hybrid of relative and fixed positioning. The element is treated as `relative` positioned until it crosses a specified threshold, at which point it is treated as `fixed` positioned.

###### References

* https://developer.mozilla.org/en/docs/Web/CSS/position

[[↑] Back to top](#css-questions)

### What existing CSS frameworks have you used locally, or in production? How would you change/improve them?

* **Bootstrap** - Slow release cycle. Bootstrap 4 has been in alpha for almost 2 years. Add a spinner button component, as it is widely used.
* **Semantic UI** - Source code structure makes theme customization extremely hard to understand. Its unconventional theming system is a pain to customize. Hardcoded config path within the vendor library. Not well-designed for overriding variables unlike in Bootstrap.
* **Bulma** - A lot of non-semantic and superfluous classes and markup required. Not backward compatible. Upgrading versions breaks the app in subtle manners.

[[↑] Back to top](#css-questions)

### Have you played around with the new CSS Flexbox or Grid specs?

Yes. Flexbox is mainly meant for 1-dimensional layouts while Grid is meant for 2-dimensional layouts.

Flexbox solves many common problems in CSS, such as vertical centering of elements within a container, sticky footer, etc. Bootstrap and Bulma are based on Flexbox, and it is probably the recommended way to create layouts these days. Have tried Flexbox before but ran into some browser incompatibility issues (Safari) in using `flex-grow`, and I had to rewrite my code using `inline-blocks` and math to calculate the widths in percentages, it wasn't a nice experience.

Grid is by far the most intuitive approach for creating grid-based layouts (it better be!) but browser support is not wide at the moment.

###### References

* https://philipwalton.github.io/solved-by-flexbox/

[[↑] Back to top](#css-questions)

### Can you explain the difference between coding a website to be responsive versus using a mobile-first strategy?

Note that these two 2 approaches are not exclusive.

Making a website responsive means the some elements will respond by adapting its size or other functionality according to the device's screen size, typically the viewport width, through CSS media queries, for example, making the font size smaller on smaller devices.

```css
@media (min-width: 601px) {
  .my-class {
    font-size: 24px;
  }
}
@media (max-width: 600px) {
  .my-class {
    font-size: 12px;
  }
}
```

A mobile-first strategy is also responsive, however it agrees we should default and define all the styles for mobile devices, and only add specific responsive rules to other devices later. Following the previous example:

```css
.my-class {
  font-size: 12px;
}

@media (min-width: 600px) {
  .my-class {
    font-size: 24px;
  }
}
```

A mobile-first strategy has 2 main advantages:

* It's more performant on mobile devices, since all the rules applied for them don't have to be validated against any media queries.
* It forces to write cleaner code in respect to responsive CSS rules.

[[↑] Back to top](#css-questions)

### How is responsive design different from adaptive design?

Both responsive and adaptive design attempt to optimize the user experience across different devices, adjusting for different viewport sizes, resolutions, usage contexts, control mechanisms, and so on.

Responsive design works on the principle of flexibility - a single fluid website that can look good on any device. Responsive websites use media queries, flexible grids, and responsive images to create a user experience that flexes and changes based on a multitude of factors. Like a single ball growing or shrinking to fit through several different hoops.

Adaptive design is more like the modern definition of progressive enhancement. Instead of one flexible design, adaptive design detects the device and other features and then provides the appropriate feature and layout based on a predefined set of viewport sizes and other characteristics. The site detects the type of device used and delivers the pre-set layout for that device. Instead of a single ball going through several different-sized hoops, you'd have several different balls to use depending on the hoop size.

Both have these methods have some issues that need to be weighed:

* Responsive design can be quite challenging, as you're essentially using a single albeit responsive layout to fit all situations. How to set the media query breakpoints is one such challenge. Do you use standardized breakpoint values? Or, do you use breakpoints that make sense to your particular layout? What if that layout changes?
* Adaptive design generally requires user agent sniffing, or DPI detection, etc., all of which can prove unreliable.

###### References

* https://developer.mozilla.org/en-US/docs/Archive/Apps/Design/UI_layout_basics/Responsive_design_versus_adaptive_design
* http://mediumwell.com/responsive-adaptive-mobile/
* https://css-tricks.com/the-difference-between-responsive-and-adaptive-design/

[[↑] Back to top](#css-questions)

### Have you ever worked with retina graphics? If so, when and what techniques did you use?

_Retina_ is just a marketing term to refer to high resolution screens with a pixel ratio bigger than 1. The key thing to know is that using a pixel ratio means these displays are emulating a lower resolution screen in order to show elements with the same size. Nowadays we consider all mobile devices _retina_ defacto displays.

Browsers by default render DOM elements according to the device resolution, except for images.

In order to have crisp, good-looking graphics that make the best of retina displays we need to use high resolution images whenever possible. However using always the highest resolution images will have an impact on performance as more bytes will need to be sent over the wire.

To overcome this problem, we can use responsive images, as specified in HTML5. It requires making available different resolution files of the same image to the browser and let it decide which image is best, using the html attribute `srcset` and optionally `sizes`, for instance:

```html
<div responsive-background-image>
  <img src="/images/test-1600.jpg"
    sizes="
      (min-width: 768px) 50vw,
      (min-width: 1024px) 66vw,
      100vw"
    srcset="
      /images/test-400.jpg 400w,
      /images/test-800.jpg 800w,
      /images/test-1200.jpg 1200w">
</div>
```

It is important to note that browsers which don't support HTML5's `srcset` (i.e. IE11) will ignore it and use `src` instead. If we really need to support IE11 and we want to provide this feature for performance reasons, we can use a JavaScript polyfill, e.g. Picturefill (link in the references).

For icons, I would also opt to use SVGs and icon fonts where possible, as they render very crisply regardless of resolution.

###### References

* https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/
* http://scottjehl.github.io/picturefill/
* https://aclaes.com/responsive-background-images-with-srcset-and-sizes/

[[↑] Back to top](#css-questions)

### Is there any reason you'd want to use `translate()` instead of `absolute` positioning, or vice-versa? And why?

`translate()` is a value of CSS `transform`. Changing `transform` or `opacity` does not trigger browser reflow or repaint but does trigger compositions; whereas changing the absolute positioning triggers `reflow`. `transform` causes the browser to create a GPU layer for the element but changing absolute positioning properties uses the CPU. Hence `translate()` is more efficient and will result in shorter paint times for smoother animations.

When using `translate()`, the element still occupies its original space (sort of like `position: relative`), unlike in changing the absolute positioning.

###### References

* https://www.paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/

[[↑] Back to top](#css-questions)

### Other Answers

* https://neal.codes/blog/front-end-interview-css-questions
* https://quizlet.com/28293152/front-end-interview-questions-css-flash-cards/
* http://peterdoes.it/2015/12/03/a-personal-exercise-front-end-job-interview-questions-and-my-answers-all/
