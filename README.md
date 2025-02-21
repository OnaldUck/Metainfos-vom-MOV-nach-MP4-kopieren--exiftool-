# Metainfos vom MOV nach MP4 kopieren (exiftool)
Aus Platzgründen konvertiere ich die MOV Videos von meinen iPhone zur MP4 (H265). So weit so gut.
Damit Geolokationdaten erhalten bleiben, damit die Videos nach dem Import hübsch auf der Karte angezeigt werden, nutze ich das EXIFTOOL.
Für einzelne Dateien klappt es gut.

```
exiftool.exe -TagsFromFile a:\1\img_0040.mov "-all:all>all:all" a:\1\mp4\img_0040.mp4 -overwrite_original -m
    1 image files updated
```

Will man es nur paar einzelne Dateien manuell, dann kann man sich das mitt eine Batschdatei helfen.

```
@echo off
title EXIF Tags kopieren - mit Strg + C abbrechen
mode 80,10
:anfang
set /p "orginal=Orginal-Datei: "
set /p "ziel=Ziel-Datei: "


rem um vom orginal MOV auf mp4 das Datum zu übertragen
c:\Tools\exiftool.exe -TagsFromFile %orginal% "-all:all>all:all" %ziel% -overwrite_original -m

echo ...und weiter gehts&echo.
goto anfang
exit
```
Das Ergebnis sieht dann wie folgt aus.

https://github.com/user-attachments/assets/9b1e33f7-7415-49ec-ae54-fa6068f3c223


Wenn man die MOV Videos in einen Unterordner MP4 mit den gleichen Namen lieg hat, so kann man alles in einen Abwasch machen.
```
FOR %%f IN ("*.mov") do exiftool.exe -TagsFromFile %%f "-all:all>all:all" .\mp4\%%~nf.mp4 -overwrite_original -m
```



