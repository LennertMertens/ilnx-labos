# Labo 2: Linux leren kennen

## Hulp zoeken

1. Hoe vraag je op de command-line documentatie op voor het *commando* `passwd`?

    ```
    $ man passwd
    ```

2. Hoe vraag je documentatie op voor het *configuratiebestand* `/etc/passwd`?

    ```
    $ man 5 passwd
    ```

3. Hoe vraag je een lijst op van alle documentatie die de string `passwd` bevat?

    ```
    $ man -k passwd
    ```

## Werken op de command-line

1. Wat is de huidige datum en uur?

    ```
    $ timedatectl
    ```

2. Wat is de huidige directory?

    ```
    $ pwd
    ```

3. Toon de inhoud van de huidige directory. De uitvoer zou er ongeveer zo moeten uit zien:

    ```
    $ ls
    Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
    ```

4. Toon de inhoud van de huidige directory, maar toon voor elk bestand meer informatie en ook "verborgen" bestanden.

    ```
    $ ls -la
    total 96
    drwx------. 14 student student 4096 Sep 24 09:14 .
    drwxr-xr-x.  3 root    root    4096 Sep 20 13:46 ..
    -rw-------.  1 student student  146 Sep 20 14:06 .bash_history
    -rw-r--r--.  1 student student   18 Mar 11  2013 .bash_logout
    -rw-r--r--.  1 student student  193 Mar 11  2013 .bash_profile
    -rw-r--r--.  1 student student  124 Mar 11  2013 .bashrc
    drwx------.  8 student student 4096 Sep 20 13:54 .cache
    drwxr-xr-x. 16 student student 4096 Sep 20 13:55 .config
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Desktop
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Documents
    drwxr-xr-x.  2 student student 4096 Sep 20 13:53 Downloads
    [...]
    ```

5. Toon de inhoud van de hoofddirectory van het Linux-systeem, ook vaak de root-directory genoemd. Geef een uitgebreide listing zoals in de vorige vraag, maar *zonder* verborgen bestanden.

    ```
    $ ls -l /
total 64
lrwxrwxrwx.   1 root root     7 Jul 13  2018 bin -> usr/bin
dr-xr-xr-x.   7 root root  4096 Feb 14 23:49 boot
drwxr-xr-x.  21 root root  4140 Feb 20 18:08 dev
drwxr-xr-x. 143 root root 12288 Feb 20 20:45 etc
drwxr-xr-x.   3 root root  4096 Feb 14 23:30 home
lrwxrwxrwx.   1 root root     7 Jul 13  2018 lib -> usr/lib
lrwxrwxrwx.   1 root root     9 Jul 13  2018 lib64 -> usr/lib64
drwx------.   2 root root 16384 Oct 25 01:56 lost+found
drwxr-xr-x.   2 root root  4096 Jul 13  2018 media
drwxr-xr-x.   2 root root  4096 Jul 13  2018 mnt
drwxr-xr-x.   2 root root  4096 Jul 13  2018 opt
dr-xr-xr-x. 217 root root     0 Feb 20 18:07 proc
dr-xr-x---.   4 root root  4096 Feb 14 23:58 root
drwxr-xr-x.  48 root root  1320 Feb 20 22:26 run
lrwxrwxrwx.   1 root root     8 Jul 13  2018 sbin -> usr/sbin
drwxr-xr-x.   2 root root  4096 Jul 13  2018 srv
dr-xr-xr-x.  13 root root     0 Feb 20 18:08 sys
drwxrwxrwt.  18 root root   400 Feb 20 22:35 tmp
drwxr-xr-x.  12 root root  4096 Oct 25 01:58 usr
drwxr-xr-x.  22 root root  4096 Oct 25 02:03 var

    ```

6. Wat betekenen volgende elementen van de uitvoer hierboven?
    - 1e kolom (bv. `drwxr-xr-x.`): permissions (user, group, other)
    - 2e kolom (getal): number of links
    - 3e kolom (bv. `root`, `student`): owner name
    - 4e kolom (bv. `root`): group name
    - 5e kolom (getal): bestandsgrootte
    - 6e - 8e kolom (datum): tijd van laatste aanpassing
    - de aanduiding `->` (bv. `bin -> usr/bin`): symbolische link

7. Hoe kan je commando's die je voordien uitgevoerd hebt terug ophalen (de "commandogeschiedenis")?

    ```
    $ history
    ```

## De plaats van bestanden op een Linux-systeem

Vul de tabel hieronder aan. In de linkerkolom vind je de namen van een directory, in de rechter het soort bestanden dat er in thuis hoort. Checken met `man 7 hier`

| Directory                         | Inhoud                                                                    |
| :---                              | :---                                                                      |
| `/bin`, `/usr/bin`                | **Essential user binaries**                                               |
| **`/usr./bin`**                   | Uitvoerbare bestanden voor systeembeheertaken                             |
| `/var`                            | **Spool and log files**                                                   |
| **`/var/tmp`**                    | Tijdelijke bestanden                                                      |
| `/opt`, `/usr/local`              | **local programs to the site**                                            |
| **`/`**                           | Home-directory van de `root` gebruiker                                    | 
| **`/home/student`**               | Home-directory van de gebruiker `student`                                 |
| **`/usr/share/man`**              | De inhoud van de man-pages                                                |
| **`/usr/share/doc`**              | Andere documentatie                                                       |
| `/lib`, `/usr/lib`, `lib64`, enz. | **Essential shared libraries and kernel modules**                         |
| **`/media`**                        | De inhoud van de installatie-cd voor Guest Additions(*)                   |
| `/dev`                            | **Device files**                                                          |
| `/proc`                           | **Virtual filesystem documenting kernel and process status as text files**|
| **`/etc`**                        | Systeemconfiguratiebestanden                                              |

(*) Je kan het insteken van de cd simuleren in het VirtualBox-venster van je VM in het menu "Devices" > "Insert Guest Additions CD image..." (of het Nederlandstalige equivalent).


## Werken met bestanden en directories

Om het verschil tussen een bestand en directory te verduidelijken, wordt in wat volgt de naam van een directory telkens afgesloten met “/”.

### Directories

Open eerst een terminalvenster, start de oefening vanuit je eigen home-directory. Ga enkel naar een andere directory als dat expliciet gevraagd wordt. Geef telkens de gevraagde commando's niet alleen om de taak uit te voeren, maar ook om te testen of dit correct gebeurd is.

In deze oefening leer je onderscheid maken tussen *relatieve* en *absolute paden*. Een *absoluut* pad begint altijd met een `/`, wat overeenkomt met de root-directory. Een *relatief* pad geldt vanaf de huidige directory.

1. Blijf in je home-directory en maak van hieruit een directory `tijdelijk/` aan onder `/tmp/`

    ```
    $ mkdir /tmp/tijdelijk
    ```

2. Verwijder deze directory meteen

    ```
    $ rmdir /tmp/tijdelijk/
    ```

3. Maak onder je home-directory een submap aan met de naam `linux/`

    ```
    $ mkdir linux
    ```

4. Ga naar deze directory

    ```
    $ cd linux/
    ```

5. Maak met één commando de subdirectory `a/b/` aan onder `linux/`. Als je nadien het commando `tree` geeft, moet je de gegeven uitvoer zien.

    ```
    $ mkdir -p a/b
    $ tree
    .
    └── a
        └── b
    2 directories, 0 files
    ```

6. Verwijder directory `b/` en daarna `a/` (in twee commando's)

    ```
    $ rmdir a/b
    $ rmdir a
    ```

7. Maak met één commando deze directorystructuur aan.

    ```
    $ mkdir -p c/{d,e}
    $ tree
    .
    └── c
        ├── d
        └── e
    3 directories, 0 files
    ```

8. Verwijder in één commando de directory `c/` en alle onderliggende

    ```
    $ rm -r c
    $ tree
    .

    0 directories, 0 files
    ```

9. Maak met één commando deze directorystructuur aan. Het is de bedoeling de opdrachtregel zo kort mogelijk te maken, dus niet alle directories apart opgeven!

    ```
    $ mkdir -p f/{g,h}/i
    $ tree
    .
    └── f
        ├── g
        │   └── i
        └── h
            └── i

    5 directories, 0 files
    ```

Behoud deze directorystructuur voor de volgende oefeningen over bestanden.

### Bestanden

1. Maak een leeg bestand aan met de naam `file1`

    ```
    $ touch file1
    ```

2. Maak een *verborgen* bestand aan met de naam `hidden`. Verborgen betekent dat je het niet kan zien met een "gewone" `ls`, maar wel met de gepaste optie.

    ```
    $ touch .hidden
    ```

3. Tik volgend commando in, leg uit wat er hier precies gebeurt, wat het effect is.

    ```
    $ echo hello world > file2
    ```

    **De tekst "hello world" wordt weggeschreven naar het nog niet bestaande bestanf file2, wanneer we dit commando uitvoerne wordt het bestand dus ook aangemaakt!:** 

4. Toon de inhoud van `file2`

    ```
    $ cat file2
    hello world
    ```

5. Kopieer `file1` naar een nieuw bestand `file3` in de huidige directory

    ```
    $ cp file1 file3
    ```

6. Kopieer `file1` naar de directory `f/` (die zou je nog moeten hebben van vorige oefening)

    ```
    $ cp file1 f/
    ```

7. Kopieer `file1` en file2 in één keer naar `f/g/`. Je zou de gegeven situatie moeten krijgen.

    ```
    $ cp file{1,2} f/g
    $ tree
    .
    ├── f
    │   ├── file1
    │   ├── g
    │   │   ├── file1
    │   │   ├── file2
    │   │   └── i
    │   └── h
    │       └── i
    ├── file1
    ├── file2
    └── file3
    ```

8. *Hernoem* `file3` naar `file4`

    ```
    $ mv file3 file4
    ```

9. Verplaats `file2` naar directory `f/`

    ```
    $ mv file2 f
    ```

10. Verplaats `file1` en `file4` in één keer naar `f/h/`. Je zou de gegeven situatie moeten krijgen.

    ```
    $ mv file{1,4} f/h
    $ tree
    .
    └── f
        ├── file1
        ├── file2
        ├── g
        │   ├── file1
        │   ├── file2
        │   └── i
        └── h
            ├── file1
            ├── file4
            └── i

    5 directories, 6 files
    ```

11. Kopieer `f/h/`, inclusief de inhoud, naar een nieuwe directory `f/j/`

    ```
    $ cp -r f/h/ f/j/
    $ tree
    .
    └── f
        ├── file1
        ├── file2
        ├── g
        │   ├── file1
        │   ├── file2
        │   └── i
        ├── h
        │   ├── file1
        │   ├── file4
        │   └── i
        └── j
            ├── file1
            ├── file4
            └── i

    7 directories, 8 files
    ```

### Pathname expansion (of *file globbing*)

Creëer in de directory `linux/` een aantal lege bestanden met de naam `filea` t/m `filed`, `file1` t/m `file9` en `file10` t/m `file19`. Hier is een trucje om dat snel te doen:

```
[student@localhost ~/linux] $ touch filea fileb filec filed
[student@localhost ~/linux] $ for i in {1..19}; do touch "file${i}"; done 
[student@localhost ~/linux] $ ls 
f       file11  file14  file17  file2  file5  file8  fileb 
file1   file12  file15  file18  file3  file6  file9  filec 
file10  file13  file16  file19  file4  file7  filea  filed 
```

Toon met `ls` telkens de gevraagde bestanden, niet meer en niet minder.

1. Alle bestanden die beginnen met `file`

    ```
    $ ls file*
    ```

2. Alle bestanden die beginnen met `file`, gevolgd door één letterteken (cijfer of letter)

    ```
    $ ls file? 
    file1  file2  file3  file4  file5  file6  file7  file8  file9  filea  fileb  filec  filed
    ```

3. Alle bestanden die beginnen met `file`, gevolgd door één letter, maar geen cijfer

    ```
    $ ls file[a-z]
    filea  fileb  filec  filed
    ```

4. Alle bestanden die beginnen met `file`, gevolgd door één cijfer, maar geen letter

    ```
    $ ls file[0-9]
    file1  file2  file3  file4  file5  file6  file7  file8  file9
    ```

5. De bestanden `file12` t/m `file16`

    ```
    $ ls file{12..16}
    file12  file13  file14  file15  file16
    ```

6. Bestandern die beginnen met `file`, *niet* gevolgd door een `1`

    ```
    $ ls file[!1]
    file2  file3  file4  file5  file6  file7  file8  file9  filea  fileb  filec  filed
    ```

### Links

Maak in de directory `linux/` twee tekstbestanden aan, met naam `tekst1a` en `tekst2a`. Beide hebben als inhoud “Dit is bestand tekst1” en “Dit is bestand tekst2”, respectievelijk.

1. Voor het volgende commando uit en geef de uitvoer:

    ```
    $ ls -l tekst*
    -rw-rw-r--. 1 student student 23 Feb 20 23:45 tekst1a
    -rw-rw-r--. 1 student student 22 Feb 20 23:46 tekst2a

    ```

2. Maak een *harde link* aan met naam `tekst1b` die verwijst naar bestand `tekst1a`

    ``` 
    $ ln tekst1a tekst1b
    ```
3. Maak een *symbolische link* aan met naam `tekst2b` die verwijst naar bestand `tekst2a`

    ```
    $ ln -s tekst2a tekst2b
    ```
4. Voor het volgende commando uit en geef de uitvoer:

    ```
    $ ls -l tekst*
    -rw-rw-r--. 2 student student 23 Feb 20 23:45 tekst1a
    -rw-rw-r--. 2 student student 23 Feb 20 23:45 tekst1b
    -rw-rw-r--. 1 student student 22 Feb 20 23:46 tekst2a
    lrwxrwxrwx. 1 student student  7 Feb 21 07:55 tekst2b -> tekst2a
    ```

5. Hoe zie je aan de uitvoer van `ls` dat `tekst1b` een harde link is en `tekst2b` een symbolische? Tip: Vergelijk met de uitvoer uit vraag 1!

    **Antwoord**: De symbolische link wordt aangeduid met een pijltje naar het gelinkte bestand

6. Verwijder de oorspronkelijke bestanden, `tekst1a` en `tekst2a`. Maak het commando zo kort mogelijk!

    ```
    $ rm tekst[1-2]a
    ```

7. Toon opnieuw de uitvoer van `ls -l tekst*`, en bekijk de inhoud van `tekst1b` en `tekst2b`. Wat valt je op?

    ```
    $ ls -l tekst*
    -rw-rw-r--. 1 student student 23 Feb 20 23:45 tekst1b
    lrwxrwxrwx. 1 student student  7 Feb 21 07:55 tekst2b -> tekst2a
    ```

    **Antwoord**: Omdat we bestand tekst2a hebben verwijderd kan de inhoud niet meer worden meegegeven omdat tekst2b een symlink is naar dit bestand!
    ```
    $ cat tekst1b 
    Dit is bestand tekst 1
    $ cat tekst2b 
    cat: tekst2b: No such file or directory
    ``` 

### Bestanden archiveren

1. Creëer in je home-directory een archief `linux.tar.bz2` van de directory `linux/` en alle inhoud.

    ```
    $ tar -cvf linux.tar.bz2 linux/
    ```

2. Verwijder nu volledig de directory `linux/`

    ```
    $ rm -r linux
    ```

3. Toon de inhoud van het archief zonder opnieuw uit te pakken

    ```
    $ tar -tvf linux.tar.bz2 
    drwxrwxr-x student/student   0 2019-02-21 07:58 linux/
    -rw-rw-r-- student/student  23 2019-02-20 23:45 linux/tekst1b
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file3
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file10
    -rw-rw-r-- student/student   0 2019-02-20 23:37 linux/filec
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file4
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file18
    drwxrwxr-x student/student   0 2019-02-20 23:10 linux/f/
    drwxrwxr-x student/student   0 2019-02-20 23:08 linux/f/g/
    -rw-rw-r-- student/student   0 2019-02-20 23:08 linux/f/g/file1
    -rw-rw-r-- student/student  12 2019-02-20 23:08 linux/f/g/file2
    drwxrwxr-x student/student   0 2019-02-20 23:03 linux/f/g/i/
    -rw-rw-r-- student/student   0 2019-02-20 23:07 linux/f/file1
    drwxrwxr-x student/student   0 2019-02-20 23:10 linux/f/j/
    -rw-rw-r-- student/student   0 2019-02-20 23:10 linux/f/j/file4
    -rw-rw-r-- student/student   0 2019-02-20 23:10 linux/f/j/file1
    drwxrwxr-x student/student   0 2019-02-20 23:10 linux/f/j/i/
    -rw-rw-r-- student/student  12 2019-02-20 23:05 linux/f/file2
    drwxrwxr-x student/student   0 2019-02-20 23:10 linux/f/h/
    -rw-rw-r-- student/student   0 2019-02-20 23:06 linux/f/h/file4
    -rw-rw-r-- student/student   0 2019-02-20 23:04 linux/f/h/file1
    drwxrwxr-x student/student   0 2019-02-20 23:03 linux/f/h/i/
    lrwxrwxrwx student/student   0 2019-02-21 07:55 linux/tekst2b -> tekst2a
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file11
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file19
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file1
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file7
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file9
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file2
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file14
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file17
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file12
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file13
    -rw-rw-r-- student/student   0 2019-02-20 23:37 linux/fileb
    -rw-rw-r-- student/student   0 2019-02-20 23:37 linux/filed
    -rw-rw-r-- student/student   0 2019-02-20 23:04 linux/.hidden   
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file8
    -rw-rw-r-- student/student   0 2019-02-20 23:37 linux/filea
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file16
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file6
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file15
    -rw-rw-r-- student/student   0 2019-02-20 23:38 linux/file5
    ```

4. Pak het archief opnieuw uit in je home-directory.

    ```
    $ tar xf linux.tar.bz2
    ```

