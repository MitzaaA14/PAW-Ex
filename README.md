# [Demo YouTube](https://youtu.be/K27lxMWs4IY)


# Intrebari ASP.NET Core Identity

## 1. De ce Logout e form POST si nu link GET?

Daca era GET, oricine putea sa te delogheze trimitandu-ti un link sau chiar un `<img src="/logout">` intr-o pagina random. Cu POST esti obligat sa faci o actiune intentionata, plus poti pune token CSRF. E o chestie de securitate de baza.

---

## 2. De ce login-ul face doi pasi?

Identity tine cont de faptul ca `UserName` si `Email` sunt lucruri diferite intern. Cauti userul dupa email, apoi te loghezi cu username-ul lui. Nu exista un singur apel cu email + parola pentru ca Identity nu gandeste asa — emailul e doar un camp de search, identificatorul real e username-ul.

---

## 3. De ce nu ajunge sa ascunzi butoanele in View?

Pentru ca ascunderea in View e doar cosmetica, nu securitate. Oricine poate da un request direct la `/Edit/5` din Postman sau browser fara sa vada vreo interfata. Fara `[Authorize]` in controller, serverul executa oricum.

Invers, daca ai `[Authorize]` dar nu ascunzi in View, butoanele apar, userul apasa si primeste 403. Merge, dar arata urat si confuzeaza lumea.

---

## 4. Ce e middleware pipeline-ul?

E lantul de componente prin care trece fiecare request. Ordinea conteaza enorm. `UseAuthentication()` trebuie sa fie primul pentru ca trebuie sa stii *cine esti* inainte sa verifici *ce ai voie sa faci*. Daca le inversezi, authorization ruleaza fara nicio identitate setata si toata lumea pare neautentificata.

---

## 5. Ce am fi facut fara Identity?

Practic totul de la zero: hashing parole, stocare useri, sesiuni, cookie-uri, protectie CSRF, lockout dupa incercari gresite, reset parola, roluri, validare email. Saptamani de implementat si multe sanse sa gresesti ceva si sa ai o vulnerabilitate.

---

## 6. Dezavantaje Identity?

- E lipit de Entity Framework, nu prea scapi de el
- Migrezi greu schema aia de useri in alt sistem
- E facut pe cookie-uri, deci pentru API / Angular / mobile trebuie configuratie extra pentru JWT
- Aduce mult overhead chiar daca nu ai nevoie de toate feature-urile
- Daca vrei ceva mai custom, te bati cu el
