---
cssclass: dashboard
banner: "![[niyas-ck-city-v08-small.jpg]]"
banner_y: 0.42
banner_x: 0.5
---

# Trackers

- 

searchType: frontmatter
searchTarget: caffeine
folder: Journal/Daily
fixedScale: 0.7
startDate: 2023-09-01
endDate: 2023-09-30
line:
lineColor: blue
title: Caffeine Tracker
yAxisLabel: Mgs
yAxisUnit: lbs
xAxisLabel: Date

- 

searchType: frontmatter
searchTarget: weight
folder: Journal/Daily
fixedScale: 0.7
startDate: 2023-09-01
endDate: 2023-09-30
line:
lineColor: blue
title: Weight Tracker
yAxisLabel: Weight
yAxisUnit: lbs
xAxisLabel: Date

- 

searchType: frontmatter
searchTarget: nofap
folder: Journal/Daily
datasetName: Nofap
fixedScale: 0.7
month:
startWeekOn: 'Mon'
color: steelblue
summary:
template: "Current streak: {{currentStreak()}} day(s)"

- 

searchType: frontmatter
searchTarget: noalcohol
folder: Journal/Daily
datasetName: NoAlcohol
fixedScale: 0.7
month:
startWeekOn: 'Mon'
color: steelblue
summary:
template: "Current streak: {{currentStreak()}} day(s)"

- 

searchType: frontmatter
searchTarget: sex
folder: Journal/Daily
datasetName: Sex
fixedScale: 0.7
month:
startWeekOn: 'Mon'
color: red
summary:
template: "Current streak: {{currentStreak()}} day(s)"

# Current Projects

- \[\[Health/caffeine_taper\]\]
- \[\[linux/RHCSA/RHCSA\]\]
- \[\[Health/raise_testosterone\]\]
- \[\[Personal/Health/Weight Loss/190_lbs_weight_goal\]\]

# Tech

- 🏡 Tech 
  - \[\[Linux\]\]
  - \[\[Networking\]\]
  - \[\[Python\]\]

# Vault Info

- 🗄️ Recent file updates `$=dv.list(dv.pages('').sort(f=>f.file.mtime.ts,"desc").limit(4).file.link)`
- 🔖 Tagged: favorite `$=dv.list(dv.pages('#favorite').sort(f=>f.file.name,"desc").limit(4).file.link)`
- 〽️ Stats 
  - File Count: `$=dv.pages().length`
  - Personal recipes: `$=dv.pages('"Family/Recipes"').length`