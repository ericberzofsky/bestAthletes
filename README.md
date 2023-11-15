# bestAthletes
SQL Queries to report the top two scores per sport
This was an interview question that plagued me for two days

# General Interview Question
Given a table of athletes, and a table of scores achieved by each athlete in each sport, create a query that returns the top two scores, per sport, along with the athletes names, sport, and score. Organize the output by Sport ascensding, and score descending

# Limits on Limits
The challenge with this problem is that what I thought was the obvious solution is not achievable due to limits on limits in MySql

## Obvious query
select sco.sport, ath.name, sco.score
from athletes as ath, scores as sco
where ath.id = sco.athlete_id
and sco.score in (select sci.scores from scores sci where sci.sport = sco.sport order by sci.score desc limit 2)

### Error obtained
This version of MySQL doesn't yet support 'LIMIT & IN/ALL/ANY/SOME subquery'

# Quick info on resolution
The easies way (well, after much headbanging) I found to solve this problem is to first match against the max score, and then to match against the max score of any scores remaining

## Caveat of this solution
This solution won't work if two athletes achieved the same high score

