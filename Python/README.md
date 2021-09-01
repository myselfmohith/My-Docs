## Contents
* [Numpy](#numpy)
* [Pandas](#pandas)

---

### Numpy

np.array() -&gt; list,set,tuple to array
np.arange(&lt;start&gt;,&lt;end&gt;,&lt;step&gt;) COntinous array
np.linspace(&lt;start&gt;,&lt;stop&gt;,&lt;numbers&gt;)
np.empty(&lt;shape&gt;,&lt;dtype&gt;)
np.zeros(&lt;shape&gt;,&lt;dtype&gt;)
np.ones(&lt;shape&gt;,&lt;dtype&gt;)


&lt;var&gt;.ndim -&gt; Gives the Dimension of the Array

* Axis 0 vertical Axis 1 Horizontal
* Accesing data from the matrix or Pandas DataFrame
  [&lt;row-start&gt;:&lt;row-end&gt;,&lt;col-start&gt;:&lt;col-end&gt;]
    While accesing -ve('-') implies from reverse

&lt;var&gt;.dtype -&gt; Gives Data type of the Array 
&lt;var&gt;.astype({Convertion text})

* Array act as Vectors so (2,3)*(5,3) =&gt; (10,9)
* When added Additon is done to all rows


=&gt; Array manuapulations
.transpose(arr, axes) or &lt;arr&gt;.T
.concatenate([&lt;array of arrys&gt;],&lt;axix&gt;) =&gt; shape should match and axis 0 is vertical and axis 1 is horizontal
.stack([&lt;arrs&gt;],&lt;axis&gt;) =&gt; appedn the new array if axis 0 and change shape
      if axis 1 change shape and split array accourding to rows and add them

      a = array([[1,2],[3,4]]) 
      b = array([[5,6],[7,8]]) 

      stack((a,b),0)
      array([[[1, 2],
        [3, 4]],

       [[5, 6],
        [7, 8]]])


      stack((a,b),1)
        array([[[1, 2],
        [5, 6]],

       [[3, 4],
        [7, 8]]])

NOTE: Mention axis else array is flatten
.insert(&lt;arr&gt;,&lt;pos&gt;,&lt;values&gt;,&lt;axis&gt;)
.delete(&lt;arr&gt;,&lt;pos&gt;,&lt;axis&gt;)
.append(&lt;arr&gt;,&lt;values&gt;,&lt;axis&gt;)
.unique(&lt;arr&gt;)
.amin(&lt;arr&gt;,&lt;axis&gt;)

These Function canbe resolved as Axis too
.sum() - Sum 
.mean() - Mean
.median() - Median
.var() - Varience
.std() - Standerd Deviation



* Map,filter,reduce functions works on arrays to

Copy vs View
.copy() Copy - no link to parent variable
.view() view - link to the parent variable
.base() give the parent of view


&lt;var&gt;.shape -&gt; gives the tuple of integers with shape
&lt;var&gt;.reshape(&lt;tuple&gt;) -&gt; Not inplace function change the shape of array from row =&gt; column
NOTE: reshape return view

np.nditer(&lt;var&gt;) -&gt; can used to loop to each element.
np.ndenumerate(&lt;var&gt;) -&gt; can used to loop with index and item (INDEX,ITEM)

np.array_split(&lt;var&gt;,&lt;Number fo arrays&gt;) -&gt; Splits the arrays into the given Number

np.where(&lt;Search Statment we reference complete array&gt;) -&gt; Search for indexes mating the condition and gives an array as outptut

&lt;var&gt;.sort() -&gt; sort the array if 2D or 3D sorts elements in row

*  If we wish to filter the array based on true or false
   We can use this &lt;var&gt;[&lt;True or false array&gt;]


.dot(&lt;m1&gt;,&lt;m2&gt;) -&gt; matrix multiplication
.vdot(&lt;matrix&gt;) -&gt; Vector Product


======== RANDOM ==========

Random means something that can not be predicted logically.

usage =&gt; from numpy import random or np.random.&lt;Respective Operations&gt;

.randint(&lt;start&gt;,&lt;end&gt;) =&gt; return integer
.randint(&lt;end&gt;,size=(&lt;tuplle shape&gt;)) =&gt; return n-Dimensional Matrix


.rand(&lt;Shape of ND Array&gt;) =&gt; Genreate random from 0 to 1
.normal(loc=&lt;mean&gt;,scale=&lt;std&gt;,size=&lt;Shape&gt;) =&gt; Normal distribution of array

.choice(&lt;Array var&gt;) =&gt; Select an element from array only 1D Array
This also has parameter choice which genrate random ND array(For each martix point choice random element) 

.choice() =&gt; also has parameter 'p' which takes the probabity of selecting the item in list
  ex - x = random.choice([3, 5, 7, 9], p=[0.1, 0.3, 0.6, 0.0], size=(100))

.suffle(&lt;Arr&gt;) =&gt; As name suggests suffle the array This INPLACE 
.permutation(&lt;Arr&gt;) =&gt; Gives shuffle array but not INPLACE


======== Matrix Library ============

.matlib
  .empty() -&gt; For empty matrix
  .ones() -&gt; for all once
  .zeros() -&gt; for all zeroes
  .eye(&lt;rows&gt;,&lt;colums&gt;) -&gt; Diagonal ones
  .identity(&lt;n-rows and cols&gt;) -&gt; Identity Matrix
  .rand(&lt;shape&gt;)
  .matrix('String') -&gt; String format &lt;row&gt;;&lt;row&gt;...


===== IO operations ===============

.save(&lt;filename&gt;,&lt;arr&gt;) -&gt; save the arry file as npy format
.load(&lt;file name&gt;) -&gt; load array to file


### Pandas

[&lt;start&gt;:&lt;end&gt;]
[&lt;start&gt;:&lt;end&gt;:&lt;step&gt;]


.Series(&lt;List&gt;,index=&lt;List for Lables&gt;) =&gt; creating Series

&gt; Length of Index list is the length of series
&gt; It is also like dictnory when accesing via index.

.read_csv('CSV FILE PATH')

.loc[&lt;row-start-name&gt;:&lt;row-end-name&gt;,&lt;col-start-name&gt;:&lt;col-end-name&gt;] - Here last element is Included in loc
.iloc[&lt;row-start&gt;:&lt;row-end&gt;,&lt;col-start&gt;:&lt;col-end&gt;] - Here last element is Discluded
.ix[] - 


.head(&lt;nrows&gt;) -&gt; first 5 rows
.tail(&lt;nrows&gt;) -&gt; last 5 rows

.info() -&gt; Gives the outline of your DataFrame such as colname,their non null values,datatypes
.describe() -&gt; Gives the Statistical data of the Dataframe or Series

.drop([&lt;Row Index&gt;]) -&gt; Remove the Row [NOT INPLACE]

.dropna() -&gt; This function removes the rows containing the Nan or null values [This is not inplace but we can change it to inplace to true]
    parms
        | subset -&gt; Only Colums to checked for Nan
        | inplace -&gt; take effect on same Dtaframe

.fillna() -&gt; If we encounter a Nan it will fill the respective value. [Best Pratice is to fill only the Numeric columns] [This is not inplace but we can change it to inplace to true]
    Ex -&gt; df[&lt;Column Name&gt;].fillna(130);

NOTE: if we access Elements from data frame we can get acces to function like '.mean() .median() .mode()'

.duplicated() -&gt; gives a series with True if row is Repeated
.drop_duplicates() -&gt; Drops the duplicated rows.


.corr() -&gt; Return dataframe with correlations of Datframe

.replace(&lt;From&gt;,&lt;to&gt;) -&gt; Same works as Replce function


* TO add a column we can use the dictornary tenique

.del(&lt;Column&gt;) -&gt; To delete the column of dataframe
    (or)
&lt;dataframe&gt;.pop(&lt;colname&gt;)

.append(&lt;Dataframe&gt;) -&gt; To appedn values to dataframe
.drop(&lt;row-index&gt;) -&gt; TO delte row from Dtaframe

&lt;s or df&gt;.values -&gt; Return An numpy Array from series or DataFrame
&lt;s or df&gt;.empty -&gt; Check wheather a series is empty


.T -&gt; Tranpose
.size -&gt; total elements in Seres or Df

.sum(&lt;axis&gt;) -&gt; Sum of Numeric values

=== Statistical Function ===
count()	Number of non-null observations
sum()	Sum of values
mean()	Mean of Values
median()	Median of Values
mode()	Mode of values
std()	Standard Deviation of the Values
min()	Minimum Value
max()	Maximum Value
abs()	Absolute Value
prod()	Product of Values
cumsum()	Cumulative Sum return df
cumprod()	Cumulative Product
cov() Covarience
.rank() Gives the rank of item in column
pct_change() Change of consecutive value percentage in column


=== loopping ===

&lt;df&gt;.iterrows() -&gt; Row wise 
&lt;df&gt;.itertupples() -&gt; Gives a tuple with rowindex at 0th.


=== Sorting ===
parms == ascending -&gt; True or False
         kind -&gt; which type of sort

&lt;df&gt;.sort_index() -&gt; Sortsthe Datfram,e according to indexes
    If we give axis 1 it sorts the column names

&lt;df&gt;.sort_values([&lt;colum names&gt;]) -&gt; Sort the column values


=== String Operations ===
&lt;df or seies&gt;.str =&gt; Module (return Series)

.contains(&lt;string pattern&gt;) -&gt; return series of True or False
.count(&lt;pattern&gt;)
.find(&lt;patter&gt;) -&gt; return series of -1 if not found else its index in string