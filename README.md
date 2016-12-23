# High Level Context Awareness: (HLCA)
<!-- make your own badges from here: http://shields.io/ -->
[![Version](https://img.shields.io/badge/mining%20minds-version%202.5-green.svg)](http://www.miningminds.re.kr/english/)
[![License](https://img.shields.io/badge/Apache%20License%20-Version%202.0-yellowgreen.svg)](https://www.apache.org/licenses/LICENSE-2.0)


--------------------------

<!-- Update the list and the main body. -->




- [1. Introduction](#1-introduction)
    - [1.1 Core Implementation](#11-core-implementation)
   
- [2. Getting started](#2-getting-Started)
    - [2.1 General Requirements](#21-general-requirements)
    - [2.2 Installation](#22-installation)
    - [2.3 Usage](#23-usage)
	
- [3. Features](#3-features)
   
- [4. Contributions](#4-contributions)
   
- [5. Author](#5-author)

- [6. License](#6-license)

<!-- Main Body of the Document -->


# 1. Introduction

SciGraph aims to represent ontologies and data described using ontologies as a Neo4j graph. SciGraph
reads ontologies with [owlapi](http://owlapi.sourceforge.net/) and ingests
ontology formats available to owlapi (OWL, RDF, OBO, TTL, etc).
Have a look at [how SciGraph translates some simple ontologies](https://github.com/SciGraph/SciGraph/wiki/Neo4jMapping).

Goals:
* OWL 2 Support
* Provide a simple, usable, Neo4j representation
* Efficient, parallel ontology ingestion
* Provide basic "vocabulary" support
* Stay domain agnostic

Non-goals:
* Create ontologies based on the graph
* Reasoning support



 
## 1.1 Core Implementation

The main project developed is Maven based Bridge and Singleton Patterns.
- Controllers:<br>
	The controllers provide bridge between contains under the package of "org.uclab.mm.kcl.edkat.controller".
	- Rule Controller:
		It plays an important role in handling the knowledge base. represented as "RulesController".
	- User Controller:
		This controller is responsible to handle the users (domain experts), which are using the knowledge authoring tool. It provides bridge between the
		views and user's model. It is implemented as "UserController".
	- Wellness Model Controller:
		We provided the intelli-sense to the domain experts on the rule editor to create rules using some controlled vocabulary. Wellness Model Concepts are
		using in creation of rules. Therefore, "WellnessModelController" handles the communication between views and wellness concepts model.
- Models:<br>
	Models is responsible for persisting and fetching the knowledge rules with corresponding conditions, conclusions, and situations from knowledge bases. The
	model contains three different packages as datamodel, dao (data access objects), and services.
	- Data Models:
		The data models are represented in different entity classes based on Rule, Conclusion, Condition, Situation, User, Wellness Concepts Model, and Wellness
		Concepts Relationships. These data models are put under the package "org.uclab.mm.kcl.edkat.datamodel".
	- DAO (Data Access Object):
		DAO handles the persistence and retrival of all knowledge artifacts such as rules, conditions, conclusions, situations, wellness concepts, and users. According to
		the standard structure of data access layer, DAO contain one interface and one correspinding implementation class for each above mentioned knowledge artifacts. For
		example, RuleDAO interface and RuleDAOImpl is the correspinding implementation class to handle the rules of knowledge base. Similarly, ConditionDAO and ConditionDAOImpl
		for conditions, ConclusionDAO and ConclusionDAO for conclusions, SituationDAO and SituationDAOImpl for situations and so on. All these data access object and handlers 
		are implemented according to Hibernate framework.
	- Services:
		These are local services to handle the communication between controllers and DAO objects and its implementation. The services also contains one interface and one 
		correspinding implementation class. For example, RuleService is interface and RuleServiceImpl is its implementation. Similarly, ConditionService and ConditionServiceImpl
		is handling conditions of a rule, ConclusionService and ConclusionServiceImpl is for conclusions of a rule and so on.
- Views:<br>
	According to spring mvc pattern, views are responsible to view the user interfaces by rendering the correspinding html. The rendered html is merged with data retrived by controllers
	using particular DAO and services. In this project, we have following three view.
	- Login View:
		The login view is responsible to authenticate the authorized users (domain expert), who have the rights to access, create, and modify the rules in the knowledge base.
	- Dasboard View:
		We have implemented the dashboard view for viewing the existing rules in the knowledge base at a single glance. The dashboard show the meta information of the rules like
		rule title, specialist name, institution, rule created date, and two button for Editing and deleting the existing rules. The domain expert can also navigate to rule editor
		by clicking "Add new rule" button.
	- Rule Editor View:
		The rule editor view is the main editor for creating new rule and updating the existing rules. This editor provides saparate slot for meta information of the rule, saparate
		slot for adding multiple conditions of a particular rule, saparate slot for multiple conclusions of the rule. The rule editor also facilitates the domain experts to select
		required conditional facts as situations. The selected situations are using by life-log monitor to find the abnormal situations of the user.
			
# 2. Getting Started

This consist of the following sub-headings. 


## 2.1 Requirements

The requirements for executing HLCA are as under:
- Java version: JDK 1.8 
- Maven: Apache-maven-3.2.2

Once you have Maven installed, verify with:

  mvn -version
  
Then run (once) this to download all the necessary dependencies:

  cd HLCA
  mvn package

You can import the project in Eclipse via
File > Import... > Existing Projects into Workspace

You can run mvn eclipse:eclipse to re-generate Eclipse .project and .classpath
files automatically from your pom.xml file.



## 2.2 Installation
- Database Intallation:
	*	Microsoft SQL Sever 2012
	*	Install the database and set its password and login id
	*	Where Server name is (local)
	*	Authentication is set to “SQL Server Authentication”
	*	Create a database with Name “MMIKATDB_V2”
	*	Select the database “MMIKATDB_V2” and right click and select new query
	*	Download the “MiningMindsIKATSchema.sql” and "MiningMindsIKATData.sql"
	*	Open the “MiningMindsIKATSchema.sql" file.
	*	Copy all the queries and paste into  new query window.
	*	Then Execute the query, it will create database with whole schema.
	*	Open the "MiningMindsIKATData.sql" file.
	*	Copy all the queries and paste into  new query window.
	*	Then Execute the query, it will import all the data of Mining Minds.
	*	Database is ready for the working
- Java and JDK setup
	JDK and JAVA_HOME
	*	Make sure JDK is installed, and “JAVA_HOME” variable is added as Windows environment variable
- Apache Maven Installation
	*	Download Apache Maven and install it
	*	Visit Maven official website, download the Maven zip file,
		for example : apache-maven-3.3.9-bin.zip. Unzip it to the folder you want to install Maven.
		(Assume you unzip to this folder – C:\Program Files\Apache\maven)
	*	Add MAVEN_HOME
	*	Add  MAVEN_HOME variables in the Windows environment, and point it to your Maven folder.
	*	Add to PATH
	*	Update PATH variable, append Maven bin folder, so that you can run the Maven’s command everywhere.
	*	Verification by running  mvn –version in the command prompt.
-Apache Tomcat Installation
	*	Goto http://tomcat.apache.org ⇒ Downloads ⇒ Tomcat 8.0 ⇒ "8.0.{xx}" (where {xx} is the latest upgrade number) ⇒ Binary Distributions ⇒ Core ⇒ "ZIP" package (e.g., "apache-tomcat-8.0.{xx}.zip", about 8 MB).
	*	Create your project directory, say "drive:\myProject" or "drive:\myProject". UNZIP the downloaded file into your project directory. Tomcat will be unzipped into directory "drive:\myProject\apache-tomcat-8.0.{xx}".
	*	For ease of use, we shall shorten and rename this directory to "drive:\myProject\tomcat".
-Build Project
	*	Download src and pom file into the appropriate project folder
	*	Start Command Prompt
	*	Change the directory to your project directory and folder
	*	Run “mvn clear install” command



## 2.3 Usage

Once environment has been setup, the user (domain expert) can use this user friendly authoring environment to manage the knowledge base by creating new rules and editing the existing rules. User can 
modify and customize the code according to their requirements. But users should follow the same spring mvc pattern and hibernate framework for updation the code.
*	Add new required table or update the existing table in database "MMIKATDB_V2".
*	Add new or update existing controller under the package "org.uclab.mm.kcl.edkat.controller"
*	Add new or update the existing views according to the requirements under the folder hierarchy src/main/webapp/WEB-INF/views according to followed pattern.

# 3. Features

Write the main features 

- Providing user-friendly environment to expert for transformation of their experiences into knowledge base. 


# 4. Contributions

-	Provide user-friendly Rule Editor to domain experts to maintain the knowledge base. 



# 5. Author

-  Name : Claudia Villalonga and Muhammad Asif Razzaq
-  email : cvillalonga@oslab.khu.ac.kr, asif.razzaq@oslab.khu.ac.kr


# 6. License

Copyright [2016] [Claudia Villalonga and Muhammad Asif Razzaq]

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
<br>
