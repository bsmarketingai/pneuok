# Pneuok.cz – kategorie „Pneumatiky“ · podklad pro Claude Design

**Zdroj:** https://www.pneuok.cz/pneumatiky/ (snímáno 8. 10. 2026)
**Cíl:** co nejvěrnější přenos stránky (layout, komponenty, responzivita, obsah). Nic nevylepšovat, nejdřív 1:1.

## 1. Co je v podkladech

| Soubor | Obsah |
|---|---|
| `screenshots/01_XXL_1920px.png` … `07_XXS_375px.png` | Celostránkové screenshoty v 7 breakpointech (1 px = 1 CSS px) |
| `pneuok-pneumatiky-assets.zip` → `assets/images/` | 139 rastrových obrázků, které stránka opravdu používá (produkty, bannery, loga v patičce) |
| `assets/icons/` | 241 SVG ikon z CSS šablony (68 z nich je na stránce použito – seznam níž) |
| `assets/images-unused/` | 28 obrázků z CSS, které se na této stránce nezobrazují (login bg apod.) – jen pro úplnost |
| `assets/manifest.csv` | Seznam všech souborů: název, typ, velikost, použito ano/ne, původní cesta na webu |
| `snapshot.html` + `snapshot-styles.css` | Offline snapshot DOM + kompletní CSS webu (bez JS). Referenční zdroj pro přesné hodnoty – třídy, rozměry, media queries |

## 2. Breakpointy (převzato přímo z CSS webu)

Web používá vlastní indikátor zařízení (`#deviceInfo`), hranice jsou:

| Název | Rozsah šířky | Screenshot ve šířce |
|---|---|---|
| **XXL** | ≥ 1440 px | 1920 |
| **XL** | 1150 – 1439 | 1300 |
| **L** | 1000 – 1149 | 1060 |
| **M** | 820 – 999 | 900 |
| **S** | 550 – 819 | 680 |
| **XS** | 420 – 549 | 480 |
| **XXS** | 0 – 419 | 375 |

Media queries: `(max-width: 419px)`, `(min-width: 420px) and (max-width: 549px)`, `(min-width: 550px) and (max-width: 819px)`, `(min-width: 820px) and (max-width: 999px)`, `(min-width: 1000px) and (max-width: 1149px)`, `(min-width: 1150px) and (max-width: 1439px)`, `(min-width: 1440px)`.

**Kontejner:** obsah je max. ~1280 px široký, vycentrovaný, boční padding ~16 px. Na XXL se vlevo a vpravo zobrazí **sticky reklamní skyscrapery** (~290 px široké: Cooper cashback / Goodyear cashback) mimo kontejner. Pod XXL nejsou.

## 3. Design tokeny

### Barvy
| Token | Hodnota | Použití |
|---|---|---|
| primary | `#0B2852` | navy – tlačítka, košík, šipky carouselu, payment bar, ikony |
| primary-30 | `#546986` | sekundární text |
| primary-75 / -90 | `#C2C9D4` / `#E7EAEE` | jemné plochy, disabled |
| nav-dark | `#0B0620` | hlavní menu (desktop), tmavé pozadí hero |
| text | `#0D0E46` | hlavní text, nadpisy, ceny |
| text-weaker | `rgba(13,14,70,.65)` | cena bez DPH, popisy |
| text-muted | `#8384AD` | rozměr pneu v kartě (např. „205/55 R16 91T Zimní“) |
| accent / yellow | `#F8CF43` | tlačítka CTA (Hledat, Zjistit cenu, košík v kartě), aktivní tab, linka pod menu, breadcrumb |
| secondary | `#E7F0FF` / `#E5EEFF` | box „Dodání…“ v kartě, qty stepper, sekundární tlačítka |
| badge Doporučujeme | `#004D6D` | štítek |
| badge Akce | `#FFB800` | štítek |
| badge Střední / Ekonomická / Protektorovaná | `#0D0E46` | štítek (Ekonomická má oranžovou ikonu/text) |
| skladem | `#33E82F` (text), ikona zelená | „Skladem > 20 ks“ |
| skladem u dodavatele | `#0040A3` | „Skladem dodavatel CZ/EU…“ |
| garance (ikona) | `#009933` | zelený kroužek „unlimited guarantee“ |
| error | `#EB3B5A` | |
| border karet | `#E6EFFD` 1 px; dlaždice kategorií `rgba(191,211,225,.25)`–`#DADBE7` | |
| footer bg | gradient velmi světle modrá → bílá (`#F3F7FE` → `#FFFFFF`) | |

### Typografie
- **Font: Poppins** (Google Fonts) – 400, 500, 600, 700, 600 italic. Základ 14 px.
- H1 hero „Pneumatiky“: 32 px / 600 / 1.2, bílá
- H2 sekcí („Nejprodávanější letní pneumatiky“): ~32 px / 700, `#0D0E46`, s čtvercovou navy ikonou (štítek s %) vlevo; na mobilu ~20 px a zalomení na 2 řádky
- Hlavní menu: 16 px / 600, bílá
- Název produktu: 14 px / 700 UPPERCASE (značka + model)
- Rozměr produktu: 14 px / 400, `#8384AD`
- Cena: 20 px / 700; cena bez DPH 12 px / 400
- Štítky: 12 px / 600, bílá
- Text odstavce: 14 px / 400 / 1.3–1.45

### Zaoblení & stíny
- `--border-radius: 7px` (tlačítka, inputy, panely); karty produktů ~10–12 px; bannery 18 px; štítky 5 px; popup 21 px; kruhové ikony 50 %
- Stíny jsou minimální: vyhledávací panel `0 17px 44px rgba(191,211,225,.45)`, chat bublina `0 5px 15px rgba(0,0,0,.35)`

## 4. Struktura stránky (shora dolů) a chování v breakpointech

### 4.1 Info lišta (otevírací doba)
Navy „tab“ se zaoblenými spodními rohy, vycentrovaný, ~900 px. Žlutá ikona „i“ + text *„Otevírací doba: Po-Pá: 7:00-16:00 | So-Ne:Zavřeno.“* 12 px bílá.
→ **XXL–M** viditelná; **S a menší skrytá**.

### 4.2 Utility řádek
- **XXL/XL:** vlevo odkazy *Autoservis · Pneuservis · Velkoobchod · Testy pneumatik · 📅 Online rezervace (bold)*; vpravo ikona porovnání (váhy), vlajka CZ + „CZ ⌄“, ikona uživatele v kruhu.
- **L/M:** vlevo telefon *+420 591 001 002* (číslo bold) a e-mail *info@pneuok.cz* s ikonami; vpravo totéž (porovnání, CZ, user).
- **S–XXS:** není.

### 4.3 Hlavní hlavička
- **XXL/XL:** logo PneuOK (≈170×60) · blok telefon + e-mail · vyhledávací pole (šedý 2px rámeček, lupa, placeholder „Zadejte hledaný výraz..“, uvnitř žluté tlačítko **Hledat**) · tlačítko **Nákupní asistent** (světle šedomodré `#DCE3ED`, AI ikona lupy s jiskrou) · navy tlačítko košíku s ikonou tašky a textem „0 produktů“.
- **L:** logo · search s Hledat · čtvercové tlačítko AI asistenta (jen ikona) · navy košík „0 produktů“ · outline tlačítko **MENU ☰**.
- **M:** logo · search · AI ikona · navy košík (jen ikona + žlutý badge „0“) · outline ☰.
- **S–XXS:** logo vlevo, vpravo 4 čtvercová tlačítka ~45×45 radius 10: lupa (outline navy), AI asistent (světlé pozadí), košík (navy + žlutý badge 0), ☰ (outline). Search je skrytý za ikonou. Hlavička je fixed/sticky.

### 4.4 Hlavní menu (mega menu kategorie)
- **XXL/XL:** tmavý pruh `#0B0620`, výška ~56 px, rovnoměrně rozložené položky: *Pneumatiky · Hliníkové disky · Plechové disky · Kompletní kola · Příslušenství · Bazar · Autodíly · Dárkové poukazy*; dole 2px žlutá linka.
- **L a menší:** schované pod MENU/☰ (off-canvas).

### 4.5 Hero kategorie
Celošířkový pruh s tmavou fotkou běhounu (`bs-bg-category.jpg`) + tmavý overlay. Breadcrumb: žlutá ikona domečku → šipka → „Pneumatiky“ (žlutá, 12 px). Pod ním H1 „Pneumatiky“. Výška ~105 px desktop, ~90 px mobil.

### 4.6 Úvodní text
*„Hledáte spolehlivé obutí pro svůj vůz? Správný výběr pneumatik pro osobní auta je klíčový nejen pro váš jízdní komfort, ale především pro bezpečnost vás i vaší posádky. Kvalitní pneu ovlivňují brzdnou dráhu, stabilitu v zatáčkách i spotřebu paliva. V naší nabídce najdete široký výběr modelů od prověřených světových výrobců, které splňují nejpřísnější evropské standardy.“*

### 4.7 Dlaždice podkategorií (10 ks)
Bílá dlaždice, 1px světlý rámeček, radius 5–7, výška ~50 px; navy ikona vozidla vlevo (~32 px), label 14 px, šedý chevron › vpravo.
Pořadí: Osobní · Dodávkové · Jeep · Motopneu · Čtyřkolky · Protektory · Nákladní · Zemědělské (Agro) · Industriální · Sekačky (Malé pneu).
Ikony: `osobni, dodavkove, suv (Jeep), motocykly, ctyrkolky, icon-protector, nakladni, zemedelske, prumyslove, sekacky_icon` (.svg v `icons/`).

| XXL | XL | L | M | S | XS | XXS |
|---|---|---|---|---|---|---|
| 6 sloupců | 6 | 4 | 3 | 2 | 2 | 1 |

### 4.8 Vyhledávání pneumatik (konfigurátor)
Bílá karta se stínem. Nahoře navy rámeček se 2 taby: **Základní vyhledávání pneumatik** (aktivní – navy s bílým vnitřním rámečkem) a **★ Oblíbené rozměry** (žlutý). Pod tím 5 selectů s labely: *Typ vozidla* (aktivní – navy šipka v kruhu), *Šířka, Profil, Ráfek, Období* (disabled – šedé šipky). Dole ilustrace 3 pneumatik s disky (`pneu-configurator.png` + spojovací linky `pneuCatConfigurator.jpg`) a světle žluté (disabled) tlačítko **Vyhledat ›** vpravo.
- **XXL–M:** 5 selectů v jednom řádku, obrázek pneu uprostřed pod nimi, Vyhledat vpravo dole.
- **S–XXS:** Typ vozidla přes celou šířku; Šířka/Profil/Ráfek ve 3 sloupcích; Období přes celou šířku; Vyhledat přes celou šířku; obrázek pneumatik skrytý. Na XS/XXS se texty tabů zalamují do 2–3 řádků.

### 4.9 Promo bannery (3× mezi carousely)
Celošířkový obrázek, radius 18, výška ~190 px (desktop) / ~140 px (mobil), bílý nadpis 32 px/600 vlevo + žluté tlačítko (radius 7, 16 px/600, text `#0D0E46`).
1. *„Bezpečné uskladnění pneumatik po celý rok.“* – **Zjistit cenu** (pneuCategory1.png)
2. *„Pravidelné čištění klimatizace se vyplatí.“* – **Rezervovat termín** (pneuCategory2.png)
3. *„Vaše auto si zaslouží jet rovně. Profesionální geometrie Hunter®“* – **Objednat termín** (banner-geometrie.jpg)

### 4.10 Produktové carousely (3×)
Nadpisy: *Nejprodávanější letní pneumatiky / zimní / celoroční*. Horizontální slider s navy šipkami (‹ ›, obdélník 30×70, radius 7) na okrajích přes karty.

| XXL | XL | L | M | S | XS | XXS |
|---|---|---|---|---|---|---|
| 4 karty | 4 | 3 | 3 | 3 | 2 | 2 |

**Produktová karta** (bílá, 1px `#E6EFFD`, radius ~10, padding 16):
1. Vlevo nahoře štítky pod sebou: *Akce* (oranžovo-žlutý, ikona %), *Doporučujeme* (petrolej, ikona), *Střední / Ekonomická / Protektorovaná* (tmavě navy, ikona hvězdy/kola). Vpravo nahoře ikony: typ vozidla (auto), sezóna (slunce = letní, vločka = zimní, slunce+vločka = celoroční), kruh „G“ (oranžovo-červený = značka Goodyear/garance) nebo zelený kroužek ∞ (doživotní záruka).
2. Fotka pneumatiky (čtverec 170×170, `object-fit: contain`, bílé pozadí).
3. Hodnocení 5 hvězd (žluté, nepovinné).
4. Název UPPERCASE bold (*COOPER COBRA G/T*), rozměr šedě (*295/50 R15 105S Letní*), *(DOT 26)* malým bold šedě.
5. Dostupnost s ikonou: zelená *Skladem > 20 ks* / modrá *Skladem dodavatel CZ > 5 ks*.
6. Světle modrý box: ikona hodin se šipkou, *Dodání **24 - 48 hodin*** / *Kdy zboží dostanu*, vpravo ikona porovnání (váhy).
7. Oddělovací linka, cena *4 660 Kč* (bold 20) a *3 851 Kč bez DPH*.
8. Qty stepper (světle modrý box: − | 1 | + v bílých čtverečcích) + žluté tlačítko s ikonou tašky.
- **XXL–M:** cena a stepper+košík v jednom řádku.
- **S–XXS:** cena nad stepperem; ikony vpravo nahoře pod sebou; box Dodání se zalamuje do 3 řádků.

### 4.11 Platební lišta
Navy pás radius 12 s bílými logy: ČSOB, Česká spořitelna, Fio, Fio banka, G Pay, QR Platba, KB, Mastercard, mBank, Raiffeisen BANK, UniCredit, VISA (v SVG/PNG v assets, `footerLogo*.png`).
XXL/XL 1 řádek · L/M 2 řádky · S–XXS 3 řádky, vycentrované. Přesahuje horní hranu patičky (napůl na bílé, napůl na světle modré).

### 4.12 Patička
Světle modrý gradient. Sloupce:
1. Logo PneuOK, **PNEU - OK shop s.r.o.**, Markvartovická 1416/2, 748 01 Hlučín, **Navigovat >** (podtržené), navy čtvercové ikony telefon/e-mail + *+420 **591 001 002***, ***info@pneuok.cz***
2. **Vše o nákupu:** Stáří pneu DOT, Testy pneumatik, Doprava, Obchodní podmínky, Zpracování osobních údajů, Reklamační řád, Reklamační dotazník, Odstoupení od smlouvy
3. **O nás:** Nejčastější dotazy, Technický rádce, Servis, Kontakty, Jak se k nám dostanete, Zpětný odběr pneumatik, Slovníček pojmů, Katalog výrobců
4. Tlačítka sociálních sítí (bílá, rámeček, radius 7): *PneuOK na Facebooku ›*, *PneuOK na Instagramu ›* (žlutý kroužek se šipkou)

Řádek certifikací/log: premio, Goodyear certifikovaný prodejce, Pirelli, Hankook, 4Fleet, Heureka Ověřeno zákazníky, Zboží.cz Ohodnoťte nás, Google ★★★★★.
Spodní lišta: *©2026- Pneuok.cz - Všechna práva vyhrazena* · *BSSHOP: e-shop napojený na Pohodu* (podtržené) · *Cookies* · vpravo navy tlačítko **Začátek stránky ⌃**.

| XXL/XL/L | M | S | XS/XXS |
|---|---|---|---|
| 4 sloupce, loga v 1 řádku, spodní lišta v 1 řádku | 3 sloupce + sociální tlačítka pod 1. sloupcem; loga 1 řádek (Google zalomený); spodní texty pod sebou vlevo, tlačítko vpravo | 1 sloupec (vše pod sebou); loga ve 2 řádcích; spodní texty pod sebou vlevo, tlačítko vpravo | 1 sloupec; loga v mřížce 2 sloupce; spodní lišta vycentrovaná pod sebou, tlačítko pod texty |

### 4.13 Plovoucí prvky
- Žlutá kruhová **chat bublina** (~64 px) vpravo dole, fixed.
- Na XXL vlevo svislé záložky *Ověřeno zákazníky* (Heureka, žlutá) a *premio* (navy) + Zboží „Ohodnoťte nás“.

## 5. Použité SVG ikony (na stránce)
Navigace a hlavička: `PneuOkLogo`, `logo-pneu-ok`, `search-query`, `SimpleSearchView_toggle`, `SimpleSearchView_ai`, `AiAssistantView_icon`, `basket`, `headerComparison`, `user-icon`, `profile`, `flag-cz`, `flag-sk`, `LocalizationPanelView_down`, `calendar-days-solid`, `phone`, `mail`, `MenuCategoriesView_menu_icon`, `MenuCategoriesView_expand/collapse`, `close_blue`, `SimpleItemView_close`
Breadcrumb a kategorie: `BreadcrumbView_home`, `BreadcrumbView_separator`, `CategoryRightArrow`, `osobni`, `dodavkove`, `suv`, `motocykly`, `ctyrkolky`, `icon-protector`, `nakladni`, `zemedelske`, `prumyslove`, `sekacky_icon`
Konfigurátor: `select-arrow`, `arrow-r`, `star_blue`, `diameter`
Produktová karta: `akce`, `doporucujeme_icon`, `icon_gold/silver/bronz`, `icon_protector`, `icon_osobni`, `icon_jeep_suv`, `icon_dodavkove_van`, `icon_letni`, `icon_zimni`, `icon_celorocni`, `unlimited_guarantee`, `availability_icon_green/blue_light/red`, `avail_info_icon`, `info-icon`, `ProductActionPanelView_compare`, `rating-color`, `rating-gray`, `PdAddToCartView_minus/plus`, `AddToCartView_button_buy`, `ProductsView_scroll_left/right`, `hp-akcni`
Ostatní: `premio`, `zboziWidget`, `GoTop`
(Čísla v názvech souborů, např. `.8080887311234653089`, jsou cache-busting verze původního webu – ignoruj je.)

## 6. Pokyny pro Claude Design
1. Postav stránku z komponent: Header (3 varianty: desktop / tablet / mobile), MegaMenu bar, CategoryHero, CategoryTile, TireSearch (konfigurátor), PromoBanner, ProductCard, ProductCarousel, PaymentBar, Footer.
2. Barvy a typografii nastav jako tokeny podle sekce 3; font Poppins.
3. Pro každý breakpoint ověř shodu se screenshotem stejného názvu (počty sloupců viz tabulky v sekci 4).
4. Obrázky a ikony používej z `assets/` – názvy odpovídají `manifest.csv` a CSS ve `snapshot-styles.css`.
5. Při nejasnosti rozhoduje `snapshot.html` + `snapshot-styles.css` (to je původní CSS webu, včetně všech media queries).
6. Chat widget (servicedesk) a skript ankety nejsou součástí snapshotu – stačí statická žlutá bublina.
