
## DVC

let's say that you have 100 GBS of data, you can't go ahead and store it in some repository, it will also be very much difficult for Git to manage that with respect to versioning.
so whenever you have this kind of huge it is always better to use DVC along with git to manage that data

## tutorial

DVC works along with git, DVC will be used for tracking data files and git will track the entire other code information

 1. **initialize DVC**    	
`dvc init`      
after initialization, any file I add, DVC will start versioning this specific file

2. **File Tracking**    		
if we want to track any code file using git we use `git add FILE` we will do the same thing here     
`dvc add data/data.txt`   
**data.txt** will not be tracked with git anymore, data.txt added by DVC to .gitignore, git will track .gitignore and **data.txt.dvc** only

**The Question raised here is what does data.txt.dvc used for ??**     		
it contains a unique hash key for data.txt file content, once you change the data.txt content, the hash key will be changed
so now we don't care about data.txt we can store it anywhere we want like the s3 bucket, we only care about data.txt.dvc    

**DVC**     		
it hashes the content of the file in the cache folder and it creates a hash key for this folder and this hash key will be saved in data.txt.dvc

![HashKey](https://github.com/ahmedbasemdev/Data-Version-Control/blob/master/Images/hash_key.png?raw=true)

3. **Staging and Local Repo**
	* `git add data/data.txt.dvc`
	* `git commit -m "Message"`		    
	
after moving data.txt.dvc to the staging area by using add command and moving it to local repo using commit command now we are able to switch between different versions of data

let's display your commits by using `git log` and take the id of commit version 2 which its name is DVC

![git log](https://github.com/ahmedbasemdev/Data-Version-Control/blob/master/Images/commits.jpg?raw=true)

`git checkout e4efcdefef9effc3017ed594ff0ae84034a5bee4`			
you check the hash key version in data.txt.dvc file, you will notice that the hash key is changed to the second version, and data.txt still the same			
**If we want to return data.txt to the second version also**		
`dvc checkout`		
it will take the reference key "hash key" will go to the cache folder and will pick up the file related to that hash key		

**Let's go back to latest version**
* `git checkout master`
* `dvc checkout`
