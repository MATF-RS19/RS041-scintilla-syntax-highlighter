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

