# Cheat sheet

**Note:** Deze cheat sheet biedt een goed overzicht van basiscomando's die beshikbaar zijn, voor verdere uitleg raadt ik aan om de man pages te raadplegen
## Belangrijke bestanden
| Taak                       | Commando      |
| :---                       | :---          |
| File met users             | `/etc/passwd` |
| File met wachtwoorden      | `/etc/shadow` |
| File met groups            | `/etc/groups` |

### Linux directorystructuur

| Taak                                                                   | Commando |
| :---                                                                   | :---     |
| Essential user command binaries                                        | `/bin/`  |
| Static files of the boot loader                                        | `/boot/` |
| Device files                                                           | `/dev/`  |
| Host specific system configuration                                     | `/etc/`  |
| User home directories                                                  | `/home/` |
| Essential shared libraries and kernel modules                          | `/lib/`  |
| Mount point for removable media                                        | `/media/`|
| Mount point for a temporarily mounted filesystems                      | `/mnt/`  |
| Add-on application software packages                                   | `/opt/`  |
| System binaries                                                        | `/sbin/` |
| Data for services provided by this system                              | `/srv/`  |
| Temporary files                                                        | `/tmp/`  |
| User utilities and applications                                        | `/usr/`  |
| Variable files                                                         | `/var/`  |
| Home directory for the root user                                       | `/root/` |
| Virtual filesystem documenting kernel and process status as text files | `/proc/` |




## Basic linux cammando's

| Taak                                  | Commando |
| :---                                  | :---     |
| Update packages                       | `sudo dnf upgrade -y` |
| Absoluut pad naar uitvoerbaar bestand | `which COMMANDO`   |
| Beschrijving krijgen van een man-page | `whatis COMMANDO`  |
| Locatie van een manpage nagaan        | `whereis COMMANDO` |
| Verplaats of hernoem bestand          | `mv BESTAND_1 BESTAND_2` |
| Update man pages                      | `sudo mandb` of `sudo makewhatis` |
| Commando historiek bekijken           | `history`                         |

## Hulp zoeken

| Taak                                          | Commando        |
| :---                                          | :---            |
| Hulp over het commando 'passwd'               | `man passwd`    |
| Hulp over configuratiebestand '/etc/passwd'   | `man 5 passwd`  |
| Zoeken in alle man-pages naar string 'passwd' | `man -k passwd` |
| man over directorystructuur                   | `man hier`      |
| Ingebouwde bash commando's                    | `man builtins`  |
| 'wildcards' in bestandsnamen                  | `man 7 glob`    |
| Info over manpages                            | `man man`       |

### Binnen man-page:

- `q` : man-page verlaten
- `/` : zoeken binnen de pagina
- `n` : ga naar volgende zoekresultaat
- `N` : ga naar vorige zoekresultaat

**Secties**
- 1 : commando's
- 5 : configuratiebestanden
- 8 : systeembeheercommando's


## Substitutie/expansie

- `Brace expansion`, vb. `{1..10}, dir/{subdir1,subdir2,subdir3} `
  - vb. `mkdir -p project/{src,lib,build}`

- `Tilde expansion`: ~ wordt vervangen door home directory, vb `/home/student/`
  - vb. `ls ~/.ssh`
  
- `Parameter expansion`: variabelenamen worden vervangen door waarde, vb/ `${USER}` => `student`

- `Command substitution`: `$(commando)` wordt vervangen door uitvoer van commando
  - vb. `date=$(date)`

- `Filename expansion` of globbing: wildcards in bestandsnamen, vb. `*`, `?`, `[abc]`, enz.
  - vb. `rm *.class`

### Resultaat expansie
- `set -x`: toont het resultaat van expansie ("debug mode")
- `set +x`: zet optie terug uit
  - Voorbeeld: `set -x; ls -ld ${HOME}/D[eo]*; set +x`


## Filters

| Taak                                             | Commando                             |
| :---                                             | :---                                 |
| Print een bestand                                | `$ cat`                              |
| Zoeken op een bepaalde string of regex           | `$ grep`                             |  
| Zoeken naar een string die de regex niet match   | `$ grep -v`                          |
| Zoeken naar een string die match case insensitie | `$ grep -i`                          |
| Toon ook één lijn na het resultaat            | `$ grep -A1 Henin tennis.txt`           |
| Toon ook één lijn voor het resultaat          | `$ grep -B1 Henin tennis.txt`           |
| Toon 3 lijnen voor en na het resultaat        | `$ grep -C3 Henin tennis.txt`           |
| Selecteer kolom 1 en 3 uit `/etc/passwd`      | `$ cut -d: -f1,3 /etc/passwd | tail -4` |
| Vervang letter 'e' door 'A'                   | `$ cat tennis.txt | tr 'e' 'E'`         |
| Verwijder alle niet  letters uit een stream   | `$  cat text | tr -d ',!$?.*&^%#@;()-'` |
| Vervang alle kleine letters doot hoofdletters | `$ cat tennis.txt | tr 'a-z' 'A-Z'`     |
| Woorden, lijnen en karakters tellen           | `$ wc -w`, `$ wc -l`, `$ wc -c`         |
| Sorteer een bestand alfabetisch               | `$ sort bestand`                        |
| Duplicates verwijderen uit een sorted list    | `$ sort bestand | uniq`                 |
| Tel aanglogde gebruikers op een systeem       | `$ who | wc -l`                         |
| Voeg regelnummers toe aan een bestand         | `$ nl bestand`                          |
|  | `` |
|  | `` |
|  | `` |
|  | `` |
|  | `` |


## Werken met tekst


| Taak                                                | Commando                                              |
| :---                                                | :---                                                  |
| Voorkomen dat `>` file overwrite met noclobber      | `$ set -o noclobber`                                  |
| noclobber functie weer uitschakelen                 | `$ set +o noclobber`                                  |
| Overruling noclobber                                | `>|`                                                  |
| Tekst toevoegen aan een bestand, append             | `>>`                                                  |
| Errors wegschrijven                                 | `2> /dev/null`                                        |
| Match het einde van een string                      | `$ grep 'a$' bestand`                                 |
| Match het begin van een string                      | `$ grep '^F' bestand`                                 |
| Vind enkel het volledige woord eg. "over"           | `$ grep \bover\b bestand` of `$ grep -w over bestand` |
| Zoek een string en vervang door een andere string   | `$ rename 's/TXT/text/' *`                            |
| eg. verander file extension                         | `$ rename 's/text/txt/' *.text`                       |
| Global replace                                      | `$ rename 's/TXT/txt/g' aTXT.TXT`                     |
| Case insensitive replace                            | `$ rename 's/.text/.txt/i' *`                         |
| Rename enkel de file extensions                     | `$ rename 's/.txt$/.TXT' *.txt`                       |
| stream editing met sed eg. vervang 'Sun' door 'Mon' | `$ echo Sunday | sed 's/Sun/Mon'`                     |
| Een `.` kan eender wat karakter voorstellen         | `$ echo 2014-04-01 | sed 's/....-..-../YYYY-MM-DD'`   |
| Vervang whitespaces door 1 space                    | `$ echo -e 'today\tis\twarm' | sed 's/\s/ /g'`        |
| Optioneel karakter eg. de derde 'o'                 | `$ grep -E 'ooo?' bestand`                            |
| Exact aantal voorkomens, eg. 3 'o'                  | `$ grep -E 'o{3}' bestand`                            |
| Minimum en maximum aantal voorkomens                | `$ grep -E 'o{2,3}' bestand`                          |
| Vim leren kennen                                    | `$ vimtutor`                                          |

### Vim survival guide

- Bij opstarten van Vim kom je terecht in *normal mode*.
- Als je tekst wil invoeren moet je naar *insert mode*.

| Taak                       | Commando |
| :---                       | :---     |
| Normal mode -> insert mode | `i`      |
| Insert mode -> normal mode | `<Esc>`  |
| Opslaan                    | `:w`     |
| Opslaan en afsluiten       | `:wq`    |
| Afsluiten zonder opslaan   | `:q!`    |


## Sources
- [Slides HoGent](https://hogenttin.github.io/ilnx-slides)
