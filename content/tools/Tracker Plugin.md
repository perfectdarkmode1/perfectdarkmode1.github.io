# three backtiks + tracker to create a tracker

https://github.com/pyrochlore/obsidian-tracker/blob/master/examples/HabitTracker.md

```tracker
searchType: frontmatter
searchTarget: noalcohol
folder: Personal/Journal/Daily
datasetName: nonoalcohol
fixedScale: 0.7
month:
	startWeekOn: 'Mon'
	color: steelblue
```
```tracker
searchType: frontmatter
searchTarget: nofap
folder: Personal/Journal/Daily
datasetName: nofap
summary:
	template: "Longest Streak: {{maxStreak()}} day(s)\nLongest Breaks: {{maxBreaks()}} day(s)\nLast streak: {{currentStreak()}} day(s)"
```

Which type of search to perform
	searchType: frontmatter
		frontmatter = YAML stuff

searchTarget: kegels
	What to search for

folder: Personal/Journal/Daily Notes
	where to search

datasetName: kegels
	add name to the chart

startDate: 2023-01-01
endDate: 2023-01-31
	set a range of dates to show
	
month: 
	What to do with the data
	startWeekOn: 'Mon'
		start each week on monday
	color: steelblue
		change tracker color
		supports hex code
	mode: annotation
	annotation: 🕴

fixedScale: 1.5
	change size of the tracker
	
summary:
	template: "Longest Streak: {{maxStreak()}} day(s)\nLongest Breaks: {{maxBreaks()}} day(s)\nLast streak: {{currentStreak()}} day(s)"
		create a summary of tracker as a separate tracker code block. Needs top 4 parameters from tracker

## Weight tracker


```tracker
searchType: frontmatter
searchTarget: weight
folder: Personal/Journal/Daily
line:
```

## Caffeine Tracker (line)

```tracker
searchType: frontmatter
searchTarget: caffeine
folder: Personal/Journal/Daily
startDate: 2023-01-01
endDate: 2023-01-31
line:
	lineColor: blue
	title: Caffeine Tracker
	yAxisLabel: caffeine
	yAxisUnit: mgs
	xAxisLabel: Date
```

## Caffeine Tracker (bar)
	- with title

```tracker
searchType: frontmatter
searchTarget: caffeine
folder: Personal/Journal/Daily
startDate: 2023-01-01
endDate: 2023-01-31
bar:
	title: Caffeine Tracker
	yAxisLabel: caffeine
	yAxisUnit: mgs
	xAxisLabel: Date
	
```

```tracker
searchType: frontmatter
searchTarget: caffeine
folder: Personal/Journal/Daily
summary:
	template: "Minimum: {{min()}}mgs\nMaximum: {{max()}}mgs\nMedian: {{median()}}mgs\nAverage: {{average()}}mgs"
```


	yAxisLabel: 
	xAxisLabel:
		Label the x and y axi

	yAxisUnit: mgs
		Add unit in () by the label

	lineColor: yellow (not working)
		changes line color

Doc for weight tracker summary
	https://github.com/pyrochlore/obsidian-tracker/blob/master/examples/WeightTracker.md

## Pomodoro Tracker

```tracker
searchType: frontmatter
searchTarget: pomodoros
folder: Personal/Journal/Daily
bar:
	title: Pomodoro Tracker
	yAxisLabel: Pomodoros
	yAxisUnit: 
	xAxisLabel: Date
```

```tracker
searchType: frontmatter
searchTarget: pomodoros
folder: Personal/Journal/Daily
summary:
    template: "Longest Streak: {{maxStreak()}} day(s)\nLongest Breaks: {{maxBreaks()}} day(s)\nLast streak: {{currentStreak()}} day(s)"
```

## Word Tracker

```tracker
searchType: fileMeta
searchTarget: numWords
folder: Personal/Journal
line:
	title: Word Counter
	yAxisLabel: Words
	lineColor: red
```

```tracker
searchType: fileMeta
searchTarget: numWords
folder: Personal/Journal
summary: 
	template: 'Total number of words: {{sum()}}'
```

## Mood Tracker

```tracker
searchType: frontmatter
searchTarget: mood
folder: Personal/Journal/Daily
startDate: 2023-01-01
endDate: 2023-01-31
line:
	title: "Mood"
	yAxisLabel: Mood
	lineColor: "#d65d0e"
```

## Pomodoros and Mood

```tracker
searchType: frontmatter
searchTarget: pomodoros, mood
folder: Personal/Journal/Daily
datasetName: pomodoros, mood
startDate: 2023-01-01
endDate: 2023-01-31
line:
	title: Pomodoros & Mood
	yAxisLabel: Pomodoros, Mood
	lineColor: yellow, red
	yAxisLocation: left, right
	showLegend: True
```

yAxisLocation: left, right
	puts second parameter on the right

datasetName: pomodoros, mood
	give name for legend to label

showLegend: True
	- add legend