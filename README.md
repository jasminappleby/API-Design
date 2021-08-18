# API Design Task

## Considerations

For this type of database, we would be want there to be relationships between the databases. With that in mind, a relational SQL database has been implemented. 

Within this scenario, we assumed the dataset would be used within a made-up letting company where Owners could log in and access their house data, update/delete tenant information. Tenants could log in as well so they can update their information as well, incase they have moved on and now own a home or they want to alter other information on their profile. 

## Schema

For our Schema Tables, we took a UNF to 3NF approach to create them. This enabled us to split up the data attributes within the database more logically. 

> Key: The top line is the header of the Schema Table. This will also be in bold. 
> PK = Primary Key
> FK = Foreign Key

UNF 				
				
|person|address|street address|
|-------|--------|----------|
|age  |owner| postcode |
|name|
|num_of_ppl|		


1NF		
		
|person		|address|
|---------------|--------|
|f_name	  	|house_number|
|l_name	  	|street|
|age	     	|city|
|num_of_ppl	|county|
|resident 	|country|
|	        |postcode|


2NF
|	|**person**|
|---------------|--------|
|pk	|persID|
|	|f_name|
|	|l_name|
|	|age|
|	|num_of_ppl|
|fk	|resID|


|	|**resident**|
|---------------|--------|
|pk	|resID|
|	|owner|
|	|tenant|



	address
pk	addressID
	house_number
	street
fk	cityID
fk	countyID
fk	countryID
	postcode


	city
pk	cityID
	city



	county
pk	countyID
	county



	country
pk	countryID
	country


3NF	
		
	person	
pk	persID	int
	f_name	varchar(50)
	l_name	varchar(50)
fk	ageID	int
	num_of_ppl	int
fk	resID	int


age		
ageID	int	
youth	int	18-24
young_adult	int	25-34
adult	int	35-59
senior	int	60+


	resident type	
pk	resID	int
	owner	boolean
	tenant	boolean


	**house**	
pk	houseID	    int
fk	addressID	  int
fk	resID	      int
    size        int



	address	
pk	addressID	int
	house_number	varchar(50)
	address_line_1	varchar(150)
	address_line_2	varchar(150)
fk	cityID	int
fk	countyID	int
fk	countryID	int
	postcode	varchar(8)
fk	houseID	int


	neighbourhood	
pk	neighbourhoodID	int
fk	addressID	int


## API Requests 


## HTTP Verbs and Paths


