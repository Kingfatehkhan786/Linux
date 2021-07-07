## How to send files over S3 bucket without storing the files on server


#### So the scenario is I want to upload the daily backup of the website which Create the code tar.gz and database tar.gz on daily basis but i dont want that the file consume server space and i want every backup which got created has the time and date tag so that i can recognize them which backup belongs to which date.


````

date=`date '+%d%b%Y'_%H%M%S`
````

##### So we have created the variable of date now we can use this var for creating backup which have Date and time tags Remember this will only work in linux or bash terminal  

##### Second step is create tar compress file of folder which we want to backup or upload to s3 bucket.

```
tar c <Folder which you want to upload at server > | gzip | aws s3 cp - s3://<link>_${date}.gz 

```

 ######  now you need to mention folder name after **tar -c** like this ./folder1 ./folder2 then you need to replace your s3 link with only **< link >** once we done with this. the command will look somthing like this



```
tar c ./folder1 ./folder2 | gzip | aws s3 cp - s3://kfklinux.com_${date}.gz 

```

##### Now lets talk about Database how we going to upload it over the s3.
###### well the same scenario will work here let have a look at the command below 


````
mysqldump -u'user_name' -p'Password' DB_name | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | gzip | aws s3 cp - s3://<>_${date}.sql.gz
````


###### all you need to replace the value like username password and DB_name and once you done with that just replace the url of **link** again now the command will look like the below on 



````
mysqldump -u'user_name' -p'Password' DB_name | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | gzip | aws s3 cp - s3://kfklinux.com_.sql.gz
````