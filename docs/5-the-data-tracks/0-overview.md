Inner loop:
1. Bucket already exists
2. ETL to get data into bucket
3. DVC tracking
4. DVC changes
5. Revert all commits, no pushes

Outer loop:
1. Init job
	- Create bucket
	- Move data into bucket
	- Init DVC
2. ETL pipeline with dvc change and git push 
3. Clone jukebox
4. Change pipeline and change fetch_data to use data version in jukebox repo