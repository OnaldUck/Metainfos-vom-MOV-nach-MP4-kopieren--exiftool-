# Metainfos vom MOV nach MP4 kopieren (exiftool)
Aus Platzgründen konvertiere ich die MOV Videos von meinen iPhone zur MP4 (H265). So weit so gut.
Damit Geolokationdaten erhalten bleiben, damit die Videos nach dem Import hübsch auf der Karte angezeigt werden, nutze ich das EXIFTOOL.
Für einzelne Dateien klappt es gut.

Ich weiß nicht was richtig(er) ist `"-all:all>all:all"` oder `-all:all`. Ich nutze die Kurzform.

```
exiftool.exe -TagsFromFile a:\1\img_0040.mov -all:all a:\1\mp4\img_0040.mp4 -overwrite_original -m
    1 image files updated
```

Will man es nur paar einzelne Dateien sind, dann kann man sich das mit einer Batschdatei helfen.

```
@echo off
title EXIF Tags kopieren - mit Strg + C abbrechen
mode 80,10
:anfang
set /p "orginal=Orginal-Datei: "
set /p "ziel=Ziel-Datei: "

rem Vom orginal MOV/HEIC auf MP4/JPG das Datum zu übertragen
c:\Tools\exiftool.exe -TagsFromFile %orginal% -all:all %ziel% -overwrite_original -m

echo ...und weiter gehts&echo.
goto anfang
exit
```

Das Ergebnis sieht dann wie folgt aus.

https://github.com/user-attachments/assets/9b1e33f7-7415-49ec-ae54-fa6068f3c223


## GPS Daten von Bild-Referenzdatei
Hier noch die Möglichkeit z.B. von einer Referenzdatei **zuHause.heic** nur die GPS-Daten an alle JPG-Dateien im Ordner zu Übertragen, ohne CreateDate oder andere zu ändern.

```
exiftool.exe -TagsFromFile zuHause.heic -GPS:GPSLatitudeRef -GPS:GPSLatitude -GPS:GPSLongitudeRef -GPS:GPSLongitude -GPS:GPSAltitudeRef -GPS:GPSAltitude  *.jpg -Overwrite_Original -m
```

## GPS-Daten von MOV zur MP4
Hier noch die Möglichkeit z.B. von einer MOV-Datei nur die GPS-Daten **GPSCoordinates** zu Übertragen und **CreateDate** vom Dateinahmen zu 
2023-10-06_15-57-09

```
c:\Tools\exiftool.exe -TagsFromFile %orginal% -GPSCoordinates  %ziel% -Overwrite_Original -m
c:\Tools\exiftool.exe "-CreateDate<Filename" %ziel% -Overwrite_Original -m
```

# Batch mehrer Dateien
Wenn man die MOV Videos in einen Unterordner MP4 mit den gleichen Namen lieg hat, so kann man alles in einen Abwasch machen.
```
FOR %%f IN ("*.mov") do exiftool.exe -TagsFromFile %%f -all:all .\mp4\%%~nf.mp4 -overwrite_original -m
```



