---
date: 2022-09-27
type: project
title: 📲 iPhone Photo Migration Project
tags:
categories:
lastMod: 2022-09-27
---
### Deletion by the month steps:

1. Put all photos from that month to a tmp album on iPhone for ease of checking
2. [OPTIONAL] With #backup app, "options -> photo albums -> tick only the new tmp album -> do "Backup Again" so a new folder with those photos will appear
4. Go to [[Synology Photos]] (PB-XS/year/month), scroll to the bottom and fix wrong date time
5. Delete unnecessary photos on web
6. Mark with tag #screenshots #favorites #notes panaroma  
7. Go though iPhone, mark favorites similar to above, delete everything else (or some favorite), keep less than 30 photos per month

Read some article about the 5GB iCloud storage can hold about 800-3500 photos, after some simple calculation, I should target to only save **20 per month**

Up to 2022-09-19 on iPhone, total 40805 photos and 416 videos. This is after cleaning up 2015/11 to 2016/03



### Progress Tracking

{{query (property number-of-photos)}}
query-table:: true
query-sort-by:: when
query-sort-desc:: false
query-properties:: [:when :number-of-photos :final-number-of-photos :photos-on-iphone :time-to-process :places :tags]

Sum of all remaining photos on iPhone: {{function (sum :photos-on-iphone)}}
Average time to process per photo: {{function (average (map (fn [x](/ (:time-to-process x)(:number-of-photos x))) result))}} 
Average pictures taken per month: {{function (average :number-of-photos)}}
