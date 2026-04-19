Link YouTube : https://youtu.be/JXMdfcS86do

1. Logout (POST vs GET)

Implementarea POST împiedică delogarea accidentală, dar și protejează utilizatorul de atacurile de tip CSRF - adică vom evita eventualele momente în care un site forțează delogarea fără ca tu să vrei. Folosind POST suntem sigur că acțiunea este una reală venită de la utilizator.

2. Procesul de Login în doi pași

ASP.NET Identity lucrează intern cu UserName, iar noi preferăm să ne logăm cu emailul. Astfel la primul pas se face traducerea emailului în username-ul corespunzător din baza de date, iar la al doilea pas facem locarea cu acel username și parola.

3. Vizibilitatea în View vs Autorizarea în Controller

Ascunderea butoanelor în View are rolul de a îmbunătăți experiența utilizatorului prin eliminarea elementelor vizuale inutile, însă securitatea reală este oferită doar de atributele [Authorize] din Controller. Dacă am omite verificarea din Controller, orice utilizator care cunoaște adresa URL a unei acțiuni ar putea să o execute manual, ignorând faptul că butonul nu este vizibil pe pagină.

4. Middleware și ordinea Authentication/Authorization

Middleware-ul reprezintă un ansamblu de componente software dispuse într-un pipeline care procesează pe rând fiecare cerere HTTP ce ajunge la server. Ordinea de apelare ar fi UseAuthentication() ca să aflăm cine ești, iar apoi ar fi UseAuthorization() ca să vedem dacă ai voie să faci ceva. Dacă ar fi puse invers, aplicația ar încerca să verifice drepturile înainte să verifice identitatea.

5. Implementarea manuală a securității

Dacă nu am utiliza Identity, ar trebui să programăm de la zero pentru tot ce ține de verificarea parolelor prin algoritmi de hashing, gestionarea cookie-urilor de sesiune și logica pentru blocarea conturilor în cazul atacurilor. De asemenea, am fi fost responsabili pentru crearea întregului sistem de resetare a parolelor și de confirmare a conturilor prin email.

6. Dezavantajele utilizării Identity

Rigiditate și tabele : Te obligă să folosești Entity Framework și îți umple baza de date cu tabele predefinite (AspNet) care sunt greu de personalizat sau de mutat pe alte tehnologii.

Probleme de compatibilitate: E construit pentru cookie-uri și pagini web clasice, fiind complicat de adaptat pentru aplicații moderne (mobile sau SPA) care folosesc token-uri JWT.
