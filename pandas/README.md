

## This is my personal collection of jupyter notebooks and notes for revison



---

# Pandas Quick Notes

- open source library built on top of numpy
- it allows fast analysis and data cleaning and preperation
- it excels in performance and productivity
- it also has built in visualization features
- it can work with data from wide variety of sources

________________________________________________________________

## Series 

	# series is very similar to an numpy array
	# it is built on top of numpy array
	
	# difference between series and array:
	
		# series can have access labels, meaning that indexed using 
		a label
	
		pandas.Series(data, index)
	
		## you can pass dictionary, python lists, numpy arrays etc as parameters
	
	you can create labeled series using a list of values and a list of labels
	or you can just pass a dictionary
	
		import numpy as np
		import pandas as pd
	
		values = [1,2,3]
		labels = ['a', 'b', 'c']
	
		dictonary = {"a", "b", "c"}
	
		series1 = pd.Series(data=values, index=labels)
	
		series2 = pd.Series(data = dictionary)

## you can also perform operations based on the index

	ser1 = pd.Series({'gagn': 50, 'kiran': 10})
	ser2 = pd.Series({'gagn': 40, 'kiran': 34, 'sorav' : 44})
	
	ser3 = ser1 + ser2
	
	# ser3 == {'gagn': 90, 'kiran': 44, sorav: NaN} 

>  pandas and numpy will always convert numbers to float to retain information



-----------------------------------------------------------------------------

## Dataframes

	it is a bunch of series sharing indexed
	
	also can be viewed as labeled matrix
	
		dataframe = pd.DataFrame(list, row_labels, columns_labels)


	# indexing of a dataframe
	
		dataframe['M'] // will output a series
	
		dataframe[['M', 'N']] // will output a dataframe with columns M and N
	
		## selecting rows
	
			dataframe.loc['W'] // will return a series of column values for that row
	
			dataframe.loc[['W', 'X']] will return a dataframe
			
			dataframe.loc[['w','x'], ['a', 'b']]


​			
			// you can also use slicing notation for labeled indexes too
			dataframe.loc['W':, 'M':]



			dataframe.iloc[index] // iloc is for indexed location
								  // in iloc you can pass normal index you are used 
								  // to pass in normal numpy array
	
			dataframe.iloc[1:, 2:]
	
			** use loc for labeled based index
			** use iloc for numeric based index




	# adding new columns in dataframes
	
		dataframe['new'] = dataframe['M'] + dataframe['N']


	# deleting columns in dataframe
	
		use dataframe.drop(column_name, axis, inplace) method
	
		dataframe.drop('new', axis=1, inplace=True)
	
		## by default it will delete rows you have to change axis to delete columns
	
		## by default pandas will not modify the dataframe
		## it will return the changed dataframe frame
		## if you want that changes appear in original dataframe
		## set inplace property to true


	+++++++++++++ 
	
	Rows are reffered to as 0 axis as they are on index 0 of shape tuple
	and same to column axis as they have index 1 on column
	
	+++++++++++++

---

## Conditional selection of dataframes

	booldf = dataframe > 0 // will return an dataframe with boolean values
				  // which will have value true where cell satisfies condition
	
	dataframe[booldf] // dataframe with only values in cell which are true in booldf
					  // other cells will have NaN as value
	
					 ___________or___________
	
	## one step process
	
	dataframe[dataframe > 0]


	## you can also filter out rows with this
	
		dataframe[dataframe['M'] > 0] 
	
		# dataframe['M' > 0] will return a series with boolean values
		# if a row encounters a NaN value that row will be deleted

---

## Multiple conditions in conditional selection

	you cannot use normal and opertor inside conditional selection
	you have to use other operators
	
	and = &, or = |
	
		dataframe[(df['M'] > 0) & (df.P < 0) | (df.C >10)]

---

## Resetting indexes

	You can reset you label indexes back to numerical indexes by using
	
		df.reset_index(inplace=true)
	
	this will make your indexes numerical and will add a new column
	named index which will have your old labeled indexes as columns

---

## Setting new index

	df.set_index('column_name', inplace=True) // this will set the column as new index
	
	## but it will not retain your old labels as reset_index does
	## instead will overwrite



-----------------------------------------------------------

## Multi index and index hierarchy

	# zip function
	
		zips columns of passed list into pairs tuples
	
		list(zip([1,2], ['a', 'b'])) // [(1,'a'), (2, 'b')]


	# creating multiIndex dataframe


		pd.MultiIndex.from_tuples(tuples_list)
	
		## creating multiIndex dataframe
	
			hierIndex = pd.DataFrame(matrix, index=[tuples_list], columns=[columns_list])


	# indexing 
	
		hierIndex.loc['G'].loc[1]

## Cross section indexing

	- DataFrame.xs(key) can be used to cut a cross section of a dataframe
	
		- data.xs(1, level='Num')

------------------------------------------------------------------

## Missing Data in DataFrames

	np.na is used to represent null values in DataFrame
	
		data = {'A': [1,2,np.na], 'B': [0,0,np.na], 'C': [1,2,3]}
	
		frame = df.DataFrame(data)
	
		frame.dropna(axis = 0) //will drop any row with NaN values
	
	# you can specify a threhold such that only that rows are ommitted
	# in which the number of not-NaN is below than the the threshold
	
		frame.dropna(thresh = 2) //rows with non-NaN values less than 2 will be dropped


	FILLING NaN values
	
		#  frame.fillna('value') is used to fill the NaN values with the specific number 	

----------------------------------------------------------------

## Groupby in pandas

	group by allows you to group together rows based of a column and perform
	an aggregate function on them
	
		df = DataFrame.groupby(<column_name>)


	# Then You can perform aggregate functions a group
	
		## df.mean() // will give you mean of numeric values for each group
	
		## df.sum()
	
		## df.std()
	
		## df.count()
	
		## df.describe() // will provide you with info about each group
						 // such as sum, count, etc
	
		## df.describe().transpose() //for nice formatting

------------------------------------------------------------------

## Concatination

	pd.concat([...list_of_dataframes], axis)

## Merging	

	pd.merge(left, right, how='inner', on='key')
	
	// similar to join but can be joined based upon a key

## join

	left.join(right, how='inner')
	
	// performs join operation based upon an index not any key

-----------------------------------------------------------------

## Operations

	# DataFrame['col'].unique() // returns numpy array of unique values
	
	# DataFrame['col'].nunique() // returns number of unique values
	
	# DataFrame['col'].value_counts() // returns how many times each unique value has appeared
	
	# DataFrame['col'].apply(customFunction) // will apply custom function on each value
	
	# DataFrame.drop('col', axis=0)
	
	# DataFrame.sort_values(by='col1') // sort by column
	
	# DataFrame.isnull() // will give boolean dataframe with null values represented
						 // by true



	Pivot tables
	
		df.pivot_table(values='col_name_values', index=['col1', 'col2'], columns=['C'])
	
		// multilevel index dataframe
	
		// values not found will be replaced by NaN

------------------------------------------------------

## Data input and output

	- we will work with 
	
		- CSV
		- Excel 
		- HTML
		- SQL
	
	- packages required: install using pip or conda
	
		* conda install sqlalchemy
		* conda install lxml
		* conda install html5lib
		* conda install BeautifulSoup4

## Reading file

	import pandas as pd
	
	pd.read_csv('filename')
	
	pd.read_[type]('filename')

## Writing files

	pd.to_csv('filename', index=False) // else it will include index as column
	 
	pd.to_[type]('filename')

## Excel files

	pandas can only import excel file data, not the formatting, macros, formulas
	and other stuff
	
	- Pandas thinks an excel file is a bunch of sheets and each sheet is a dataframe
	
		pd.read_excel('filename.xlsx', sheet_name="sheet1")


	writing:
	
		df.to_excel('example2.xlsx', sheet_name="gagandeep singh")

## HTML:

	pd.read_html('url') // it will convert table markup to dataframe

## Sql
​	you should use sql flavour specific package to import data from sql
​	pandas is not the best way to import data from sql

		creating an sql engine in pandas
			from sqlalchemy import create_engine
	
			engine = create_engine("sqlite:///:memory:")
				// this will create a small sql engine in memory
	
			- writing data
	
				DataFrame.to_sql('databaseName', engine)
	
			- Reading data
	
				DataFrame.read_sql('databasename', con=engine) //con means connection