Link YouTube : https://youtu.be/JXMdfcS86do

1. Logout (POST vs GET)

Implementarea logout-ului ca formular de tip POST este o măsură de securitate esențială pentru a preveni deconectarea accidentală a utilizatorului prin mecanismele de prefetching ale browserelor. Dacă logout-ul ar fi un simplu link GET, site-ul ar deveni vulnerabil la atacuri de tip CSRF, unde un site ar putea forța închiderea sesiunii tale fără acordul tău.

2. Procesul de Login în doi pași

Logarea necesită doi pași deoarece ASP.NET Core Identity utilizează UserName ca identificator principal, în timp ce utilizatorii preferă să folosească adresa de Email. Astfel, la primul pas identificăm utilizatorul după email pentru a-i obține numele de utilizator, iar la al doilea pas verificăm parola, păstrând diferența dintre email (adresă de contact) și username (identificator unic în sistem).

3. Vizibilitatea în View vs Autorizarea în Controller

Ascunderea butoanelor în View are rolul de a îmbunătăți experiența utilizatorului prin eliminarea elementelor vizuale inutile, însă securitatea reală este oferită doar de atributele [Authorize] din Controller. Dacă am omite verificarea din Controller, orice utilizator care cunoaște adresa URL a unei acțiuni ar putea să o execute manual, ignorând faptul că butonul nu este vizibil pe pagină.

4. Middleware și ordinea Authentication/Authorization

Middleware-ul reprezintă un ansamblu de componente software dispuse într-o conductă (pipeline) care procesează pe rând fiecare cerere HTTP ce ajunge la server. UseAuthentication trebuie să fie apelat înaintea lui UseAuthorization deoarece aplicația trebuie mai întâi să identifice identitatea utilizatorului înainte de a putea decide ce drepturi de acces are acesta asupra resurselor.

5. Implementarea manuală a securității

Dacă nu am utiliza ASP.NET Core Identity, ar trebui să programăm de la zero mecanisme complexe pentru criptarea și verificarea parolelor prin algoritmi de hashing, gestionarea securizată a cookie-urilor de sesiune și logica pentru blocarea conturilor în cazul atacurilor de tip brute force. De asemenea, am fi fost responsabili pentru crearea întregului sistem de resetare a parolelor și de confirmare a conturilor prin email.

6. Dezavantajele utilizării Identity

Un dezavantaj major al Identity este rigiditatea schemei bazei de date, care te forțează să folosești o structură de tabele predefinită și este strâns legată de tehnologia Entity Framework. Totodată, sistemul este optimizat nativ pentru aplicații web bazate pe cookie-uri, ceea ce face configurarea lui pentru aplicații mobile sau frontend-uri moderne (care utilizează token-uri JWT) să fie mult mai dificilă.
