# RS041-scintilla-syntax-highlighter
Scintilla syntax highlighter

## Razvoj projekta se moze pratiti na mom nezvanicnom scintilla-scite repozitorijumu:

https://github.com/dusan96/scintilla-scite

# Izvestaj 1

## Uspostavljanje komunikacije

Uspostavljena je komunikacija sa ljudima koji ucestvuju u razvoju scintilla projekta pri cemu se glavna komunikacija odvija sa Randy Kramer rhkramer@gmail.com cija je i ideja razvoja oznacivanja sintakse za Mbox i TWiki/FossWiki.

## Upoznavanje sa scintilla i scite izvonim kodom i dokumentacijom projekta.

Izvorni kod za scintilla i scite projekte mogu se naci na oficijalnom scintilla sajtu https://www.scintilla.org ili na https://sourceforge.net/projects/scintilla gde su hostovani projekti koji koriste sistem Mercurial SCM https://www.mercurial-scm.org . Doprinos projektu se vrsi putem sistema patch-eva gde se vrsi revizija koda tek kada je on kompletan pa je iz toga razloga otvoren i github repozitorijum https://github.com/dusan96/scintilla-scite na kojem cu kaciti izmene na scntilla-scite projektu radi lakseg pracenja izmena u kodu i kontrole verzija koda.

## Razvoj probnog leksera za probu povezivanja scintilla baze i scite editora

Pracenjem upustva iz dokumentacije kreiran je probni lekser koji sve reci boji u crvenu boju i komentare izmedju (* *) znakova boji u plavu boju. Uz manje poteskoce uspelo je povezivanje sa scite editorom u kojem je ubacena opcija za MBox u opciji Languages koja prilikom selekcije markira tekst po pravilima iz gore navedenog probnog leksera koji funkcionise.


# Izvestaj 2

## Prepoznavanje i obelezavanje From, Date i Subject linija

Posle uspesnog test leksera razvijanje leksera za MBox header je u fazi razvoja. Trenutno lekser prepoznaje linije From, Date i Subject i oznacava ih.
#### From linija je u  formatu:
From kljucna rec za kojom sledi rec bez razmaka ili vise reci pod znacima navoda nakon kojih je datum u formatu skraceno ime dana(Mon, Thu, ...), skraceno ime meseca(Jan, Feb, ...),  dd dan u mesecu(01, 02, ...), hh:mm:ss vreme(01:01:01, ...), yyyy godina(2017, 2018, ...).
#### Date linija je u formatu:
Date: kljucna rec za kojom sledi datum u formatu dd/mm/yy nakon cega je vreme u dvanaestocasovnom formatu hh:mm i oznaka doba dana am ili pm.
#### Subject linija je u formatu:
Subject: kjucna rec za kojom sledi prazna rec ili jedna ili vise reci.

Lekser je uspesno povezan sa SciTe editorom i pri ucitavanju fajla sa ekstenzijom mbox oznacava validne linije ukoliko postoje. Takodje lekser se moze pokrenuti kada u glavnom meniju editora kliknemo na opciju Languages i izaberemo MBox.

## Problemi sa neispravnim redosledom linija

Lekser trenutno oznacava i prihvata gore navedene linije u bilo kojem redosledu i bilo gde u fajlu. Obavezan redosled je From linija za kojom sledi Date linija za kojom sledi Subject linija za kojom opciono sledi jedna ili vise linija u formatu KEYWORD:VALUE i na kraju svih linija prazna linija nakon cega se nalazi tekst sve do sledeceg validno formiranog MBox zaglavlja.


# Izvestaj 3

## Prepoznavanje validnog MBox zaglavlja

Lekser uspesno moze da prepozna validno MBox zaglavlje koje je za sada definisano kao sto je prethodno navedeno ali ce se preci na qmail standard za MBox http://www.qmail.org/qmail-manual-html/man5/mbox.html koji je ujedno i jedan od zvanicnih standara.

## Problem sa performansama leksera

Lekser za sada radi kao sto je ocekivano na manjim fajlovima, ali prilikom ucitavanje fajlova vece velicine (10mb ili vise) primetne su lose performanse koje onemogucavaju normalan rad u editoru.
Problem nastaje jer pri svakom pozivanju leksera on obradjuje kompletan fajl sto je funkcionalno za fajlove manje velicine. Zbog obradjivanja i nekih sintaksickih osobina MBox zaglavlja to je bilo privremeno resenje. Trenutno je ideja da se pribegne inkremntalnom oznacivanju fajla gde ce se oznacavati samo delovi koji su vidjivi u prozoru editora i jos neke dodatne linije ukoliko je to potrebno i prethodno oznacene linije se nece ponovo oznacivati sve dok se ne izmeni neki njihov deo.
Pokusano je implementirati ideju ali zbog nepoznatih uticaja dela koda lekser nije pozivan od strane editora kada je potrebno na primer kada korisnik skroluje dokument ostali delovi osim dala koji je prvi bio vidljiv ostaju neoznaceni.


# Izvestaj 4

## Resen problem sa efikasnoscu leksera

Lekser sada uspesno obradjuje vece fajlove (testirano na fajlu od oko 100mb), ali jos uvek dolazi do malo duzeg odziva leksera prilikom velike kolicine skrola na desnom panelu (skrolovanje pomocu misa funkcionise efikasno).
Problem je resen dopunjenom inkrementalnom metodom koja je ranije navedena tako da sada lekser obradjuje tekst koji je vidljiv i nalazi se izmedju prethodnog validnog MBox zaglavlja i narednog zaglavlja, takodje vec oznaceni delovi se ne obradjuju dok ne dodje do izmene.

## Dalje poboljsavanje efikasnosti

Iako lekser sada obradjuje samo deo teksta koji je neophodan mapa stanja koja cuva oznaku linija teksta svaki put mora da se cela azurira sto takodje trosi izvesnu kolicinu vremena. Ideja je slicna kao i za obradu teksta tj. da se omugici samo obrada oznaka linija koje su izmenjene ili na neki nacin uticu na liniju koja je oznacena i obratno( npr. izmena Subject linije ukoliko postane nepravilno zapisana moze dovesti do potrebe za izmenjivanje oznake prethodnih Date i From linija ).

# Izvestaj 5

## Prepoznavanje validnog MBox zaglavlja

Lexer trenutno prepoznaje validno MBox zaglavlje opisano na http://www.qmail.org/qmail-manual-html/man5/mbox.html. Po definiciji validno MBox zaglavlje sastoji se od prazne linije (osim ako je pocetak fajla) pracene From linijom prethodno definisanom za kojom sledi sekvenca linija u formatu <kljucna_rec>: <vrednost> bez blanko linija, i zavrsava se praznom linijom.
