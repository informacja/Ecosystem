# Welcome everyone
Today, in my opinion, the Internet browser is much more important than the operating system you use. Tell me what browser you use, and I will tell you who you are 😉
> Priority of time spent at work (programs window order on monitors):
> 1. Editor
> 2. Browser
> 3. Communicator

## Programs list
| Category                       | Name    | Link                                                       | Platform              |
|--------------------------------|---------|------------------------------------------------------------|-----------------------|
| Browser                        | [Opera](#opera)   | https://www.opera.com/pl/download                | Windows, Linux, macOS |
| Editor                         | VS Code           | https://code.visualstudio.com                    | Windows, Linux, macOS |
| Mail client                    | Thunderbird       | https://www.thunderbird.net                      | Windows, Linux, macOS |
| Screen recorder / auto publish | [ShareX](#ShareX) | https://getsharex.com/downloads                  | Windows               |

More subiective list
----------------
- Multicommander
- Github Desktop
- ConEmu
- [Tomighty](https://tomighty.github.io)



Quantity:tomato::tomato::tomato::tomato: (tomato represent estimation point)

Time planning 
===============
###### Two ways of making Checklist (put mark on left or right side to writen task)
| Quality                       | Quantity    | 
|-------------------------|--|
|- [x] Quality <br> - [x] Done <br> - [ ] Next task |Quantity :tomato::tomato::tomato::tomato:<br>Other plan :tomato::tomato:<br>(tomato represent estimation point)|
|**Examle in real world**||
| Space | Tomighty|
|![Space](docs/qualityShort.png)|![Tomighty](docs/quantity.jpg)

*Najczęstszy błąd: założenie że nie potrzebujemy odpoczynku, zmęczenie materiału*
The most frequent mistake, thinking don't need a rest

*Konspekty w Operze*

Are you interested in how to make instructions like this? Check it [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

## Screenshots

### Opera

>###### Mouse Gestures (with Right Mouse Click) 
>
> ![ddd](docs/operaclose.gif)
> [Firefox](https://addons.mozilla.org/pl/firefox/addon/opera-gestures)
> [Chrome](https://www.google.com/search?safe=active&client=opera&hs=sI7&sxsrf=ALeKk01YUHIbZmO3I4BPpMMtxpQm1mdmpQ%3A1590060053822&ei=FWTGXtaUMe70qwHU0peIDg&q=google+chrome+gestures&oq=Google+chrome+gest&gs_lcp=CgZwc3ktYWIQAxgAMgUIABDLATIFCAAQywEyBQgAEMsBMgUIABDLATIFCAAQywEyCQgAEBYQHhCLAzIJCAAQFhAeEIsDMgkIABAWEB4QiwMyCQgAEBYQHhCLAzIJCAAQFhAeEIsDOgQIIxAnOgYIIxAnEBM6BAgAEEM6CAgAEIMBEIsDOgoIABCDARBDEIsDOgcIABBDEIsDOgUIABCLAzoFCAAQgwE6AggAOgcIABAKEIsDOggIABDLARCLA1DkBVj0NGC6O2gBcAB4AIABtwGIAecRkgEEMC4xOZgBAKABAaoBB2d3cy13aXq4AQM&sclient=psy-ab)

###### Search in browser tabs
![why](docs/operatabs.gif)

###### [Flow](https://help.opera.com/pl/touch/my-flow/)

###### Send pages to Opera Touch in your phone 
![why](docs/flow.jpg)

### ShareX 

###### Screen capture, file sharing and productivity tool
![why](docs/whysharex.png)

###### Lookup of possibilities
![why](docs/sharex.gif)


#### Tomighty 
###### Pomodoro method - *nabieranie właściwych nawyków, a umiejętność oderwania się od zadania jest pożądana u programistów*
![why](docs/tomighty.png)

-------------------------------------

> Wybierz studentów którzy przynależa do wojska, wypisz ich kierunek studiów, fakultet na jaki są zapisani oraz ich 
> prowadzącego fakultet

```sql

WITH 
  fakultety AS
    (SELECT s.nr_albumu,
            ks.nazwa_kierunku,
            f.nazwa_fakultetu,
            f.id_fakultetu
     FROM dziekanat.studenci s
     LEFT OUTER JOIN dziekanat.studenci_kierunkow sk USING(nr_albumu)
     LEFT OUTER JOIN dziekanat.kierunki_studiow ks ON ks.id_kierunku = sk.id_kierunku_studiow
     LEFT OUTER JOIN dziekanat.zapisy USING(id_kierunku_studiow)
     NATURAL JOIN dziekanat.fakultety f
     GROUP BY s.nr_albumu, ks.nazwa_kierunku, f.nazwa_fakultetu, f.id_fakultetu),
  poborowi AS
    (SELECT nr_albumu,
	 		wku
     FROM dziekanat.wojsko
     INNER JOIN dziekanat.studenci USING (nr_albumu)
     WHERE wku = 'WKU w Tarnowie'),
  prowadzacy as
    (SELECT pr.id_prowadzacego,
            pr.imie,
            f.id_fakultetu,
            f.nazwa_fakultetu
     FROM kadry.prowadzacy pr
     LEFT OUTER JOIN dziekanat.fakultety f USING(id_prowadzacego)
     WHERE f.nazwa_fakultetu IS NOT NULL )
	 
SELECT *
FROM fakultety f
LEFT OUTER JOIN prowadzacy USING (id_fakultetu)
LEFT OUTER JOIN poborowi USING (nr_albumu)
WHERE wku IS NOT NULL AND id_fakultetu IS NOT NULL;


```