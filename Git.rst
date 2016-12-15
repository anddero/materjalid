Git
====

Git on versioonihaldustarkvara, mis võimaldab koodis tehtud muudatusi säilitada ning neile ligi pääseda erinevatest arvutitest. 
Git on võimalik alla laadida järgnevalt leheküljelt: https://git-for-windows.github.io/ (kui operatsioonisüsteemiks on Mac OS X, siis pole vaja enamasti Git'i tarvis installeerida, see on juba arvutis vaikimisi olemas koos Xcode'iga. Olemasolu saab kontrollida, kui kirjutada Terminali *git --version*).
Windows'is on käskude jooksutamiseks *Git Bash*, Mac OS X'is *Terminal*.

.. image:: https://explainxkcd.com/wiki/images/4/4d/git.png

Esmakordsel *Git Bashi*' käivitamisel tuleb kindlasti seadistada e-posti aadress, kuhu hakatakse *Git*'iga seotud teateid saatma. Lihtsaim moodus on kirjutada käsureale järgnev käsk:

.. code-block::

  git config --global user.email john@example.com
  
Ülaltoodud käsus tuleks asendada "john@example.com" enda reaalse kasutatava e-posti aadressiga. Kontrollimaks, kas e-posti aadress on õigesti omistatud Git'ile, tuleks käsureale kirjutada käsk:

.. code-block::

  git config --global user.email

Peale käsu andmist kuvatakse e-posti aadress, kuhu hakatakse teateid saatma.


Navigeerimine kaustade vahel
--------------------------------------------------------------
Soovituslik oleks käsureale kirjutada käsk *pwd* (print working directory), mis näitab, millises kaustas hetkel viibime.
Trükkides käsureale *ls* (list directory contents), kuvatakse meile kausta sisu (kaustade ning failide nimetused), kus hetkel viibime.
Kaustade vahel navigeerimiseks on käsk *cd* (change directory). Uue kausta loomiseks on käsk *mkdir* (make directory).


Git repositooriumi loomine
------------------------------------
Esmalt tuleks navigeerida kausta, kuhu tahetakse Git'i repositooriumi luua. Seejärel tuleks käsureal sisestada käsk:

.. code-block:: git

  git init
  
See käsk loob alamkausta nimega .git, mis sisaldab kõiki vajalikke repositooriumi faile.

Git repositooriumi kloonimine
-----------------------------
Esmakordseks salve kopeerimiseks.

.. code-block:: git

  git clone username@host:/path/to/repository
  
Failide lisamine
----------------

Ühe faili lisamine:

.. code-block:: git

  git add <faili_nimi>
  
Kõikide failide lisamine:

.. code-block:: git
  
  git add *
  
Failide kustutamine:

.. code-block:: git

  git rm <faili_nimi>

Muudatuste registreerimine
--------------------------

.. code-block:: git

  git commit -m "lühike kommentaar tehtud muudatuste kohta"

Muudatuste üles laadimine serverisse
------------------------------------

.. code-block:: git

  git push origin master
  
Commit käsk registreerib muudatused aga alles *push* käsk laeb need serverisse üles. *master*'i võib muuta mistahes teiseks haruks, kuhu tahetakse muudatusi lükata. Kui on vaja vaadata, milliseid faile on muudetud, ning mida on vaja Git'i lisada või muudatusi registreerida, siis selleks on käsk:

.. code-block:: git

  git status

Muudatuste allalaadimine serverist ja kohalike muudatuste integreerimine
---------------------------------------------------------------------------

.. code-block:: git

  git pull

Git'i kasutamine TTÜs
----------------------

Sammud projekti Git'i panemisel:

.. code-block:: git

  git clone https://uniid@git.ttu.ee/ained/iti0011/uniid.git
  
Repostiooriumi kloonimine enda arvutisse, kus *uniid* tuleb **asendada** enda Uni-ID-ga. Ainekood (iti0011) tuleks asendada vastava aine ainekoodiga.

Kui millegi pärast ei õnnestu repositooriumi kloonimine, siis tuleks kontrollida, kas kasutate ikka **https://** protokolli, mitte http://. Tuleks ka kontrollida, kas olete uniid ja parooli õigesti sisestanud (suur- ja väiketähed on erinevad!).

.. code-block:: git

  cd uniid
  
  mkdir EX00
  
  cd EX00
  
Siia kausta tuleks nüüd luua fail, näiteks *Main.java*.

.. code-block:: git

  git add Main.java
  
  git commit -m "Lühike kommentaar koodi lisamise kohta"
  
  git push origin master
  
Tulemusena peaks tulema e-maili aadressile (mail.ttu.ee) kiri õnnestumise või ebaõnnestumise kohta, õnnestumise korral ka automaattestide tulemused. Peale tagasiside saamist võib funktsiooni täiendada, et vastus õige oleks. Sellisel juhul on vaja kood uuesti Git'i üles laadida:

.. code-block:: git

  git add Main.java
  
  git commit -m "Lühike kommentaar tehtud muudatuste kohta"
  
  git push origin master

  
Probleemide vältimiseks tuleks alati enne koodimuudatusi teha repositooriumile *git pull*. See tõmbab uusima versiooni serverist. Kui see samm jääb tegemata, võib juhtuda, et failide seis arvutis läheb konflikti serveris oleva seisuga.


  
Sisseehitatud graafiline kasutajaliides
--------------------------------------------
Graafiline kasutajaliides näitab mugavalt ja graafiliselt välja ajaloo: muudatuste üleslaadimised serverisse koos aja ja kommentaariga, tehtud muudatused failis, harud jpm. Käsureal käsk:

.. code-block:: git

  gitk
  
Harud
------
Harusid kasutatakse, et viia paraleelselt sisse muudatusi, mis on teineteisest isoleeritud. *master* haru on vaikimisi haru repositooriumi loomisel. Teisi harusid on mõistlik kasutada arendamiseks ja seejärel *master* haruga ühendamiseks (*merge*), kui arendus on lõpetatud.

.. image:: https://www.atlassian.com/git/images/tutorials/collaborating/using-branches/01.svg

Kõikide repositooriumis olevate harude loetelu saamine:

.. code-block:: git

  git branch
  
Loo uus haru (asenda <haru_nimi> uue haru nimetusega):

.. code-block:: git

  git branch <haru_nimi>
  
Kustuta haru (Git ei lase kustutada haru, kui selles on salvestamata muudatusi):

.. code-block:: git

  git branch -d <haru_nimi>
  
Loo uus haru <haru_nimi> ja vahetu sellele:

.. code-block:: git

  git checkout -b <haru_nimi>
 
Vahetu tagasi *master* harule:

.. code-block:: git

  git checkout master
  
Ühenda teine haru oma aktiivse haruga (näiteks *master*):

.. code-block:: git

  git merge <haru_nimi>
  
Git üritab automaatselt ühendada muudatusi. Vahel pole see aga võimalik ja tekivad konfliktid. Sellisel juhul tuleb näidatud faile manuaalselt muuta ja uuesti lisada. 

----------

Kasulikke linke:

http://rogerdudler.github.io/git-guide/

https://www.atlassian.com/git/tutorials/what-is-git

https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control
  
