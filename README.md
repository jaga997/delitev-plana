# Delitev plana

- **admin.html** je stran za vodjo. Tukaj izbereš trgovino in mesec, uvoziš urnik, razdeliš plan in ga objaviš agentom. Prijava je s povezavo, ki pride na e-naslov tvojega računa Supabase.
- **index.html** je stran za agente. Agent se prijavi s svojim e-naslovom in osebno 6-mestno kodo ter vidi samo svoj plan, ki si ga lahko prenese kot PDF.

## Kako agent dobi dostop

1. V tabeli »Plan po agentih« vpiši e-pošto agenta.
2. Klikni **Objavi agentom**. Vsak agent dobi osebno kodo, ki se izpiše pod njegovim e-naslovom.
3. Agentu pošlji njegov osebni PDF (gumb **PDF** v njegovi vrstici). Na dnu so povezava, e-naslov in koda.

Gumb **nova** ob kodi ustvari novo kodo, stara takoj preneha delovati. Po 8 napačnih poskusih se prijava za tisti e-naslov zaklene za 15 minut.

## Kaj je v bazi

V bazi so samo objavljeni osebni plani in šifrirane kode. Urniki in delitev ostanejo v brskalniku vodje. Agent ne vidi plana trgovine ali planov drugih agentov, to zagotavljajo pravila v bazi (`supabase.sql`).

## Postavitev

1. **Supabase:** nov projekt (regija Frankfurt). V SQL Editor zaženi `supabase.sql`, prej v zadnjo vrstico vpiši e-naslov svojega računa Supabase.
2. **Supabase → Authentication → URL Configuration → Site URL:** naslov strani, npr. `https://<uporabnik>.github.io/delitev-plana/admin.html`.
3. **config.js:** vpiši Project URL in ključ `anon public` (Supabase → Project Settings → API). Ključ `anon public` je namenjen brskalniku, podatke ščitijo pravila v bazi.
4. **GitHub Pages:** repozitorij → Settings → Pages → Deploy from a branch → `main` / root.

**Dodatni vodje:** povabi jih v projekt Supabase (Project → Team) in zanje zaženi
`insert into public.admins (email) values ('vodja@podjetje.si');`

## Varstvo podatkov

V bazi so imena in e-naslovi zaposlenih ter njihovi delovni dnevi. Pred uporabo preveri z IT ali pooblaščencem za varstvo podatkov, ali smete uporabljati Supabase in GitHub.
