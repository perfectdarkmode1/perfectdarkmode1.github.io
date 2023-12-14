Dataview Documentation https://blacksmithgu.github.io/obsidian-dataview/annotation/add-metadata/
Blog post https://dannyhatcher.com/obsidian-dataview-for-beginners/

Install plugin > enable top 3 Js settings > turn on task settings

three "`" with "dataview" next to them.

```dataview
```

add table, list, task, or calendar

- Parameters are case sensitive

### Table

#### From
from "PerfectDarkMode/Books/Reading List"
- Us full filepath to grab file
- can use folder or file
	AND
		from PerfectDarkMode/Books/Reading List and perfectdarkmode
	OR
		add or for either or
		from PerfectDarkMode/Books/Reading List and perfectdarkmode
	"-"
		Add dash to exclude the specified results
			- from PerfectDarkMode/Books/Reading
	Stacking
		from PerfectDarkMode/Books/Reading List and perfectdarkmode or personal

#### Where
where file.name = "Reading List"
- Works in all 3 querys
- Pick specific file without changing the source
- Not equal
	- where file.name!= "Reading List"
	- 

file.size
	- add file size column

sort file.ctime (asc or desc)

Change names of table columns
- append with 
	- as "namehere"
	- table file.ctime as "Date Created"
Remove ID
	table without id file.link, file.ctime as "creation time"

```dataview
table Evergreen_Notes
```



```dataview
table file.ctime as "Date Created"
from "PerfectDarkMode/Books"
sort file.ctime desc
```

### List

```dataview
list file.ctime
```

### Task
file.ctime does not work here
tasks ask for different information than tables or lists

Group tasks
	- group by status

```dataview
task
group by status
```

[  ] makes a task (with a - before it)
- [x] Example task ✅ 2023-01-10
- [ ] Task 2
- [ ] Task 3
- [ ] 