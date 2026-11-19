# BroRider#
CLAUDE.md - Biblia Proiectului: "BroRider" (Parodie Urbană România)

## 1. Prezentarea Generală a Proiectului
- **Titlu provizoriu:** BroRider (parodie satirică, 100% originală pentru a respecta legea satirei și a evita problemele de copyright/DMCA pe Steam).
- **Gen:** Arcade / Comedy / Urban Chaos Simulator (3D Third-Person, cu mod opțional GoPro/Action Cam).
- **Platformă țintă:** PC (Steam - Steamworks).
- **Motor Grafic:** Unity 6 (Universal Render Pipeline - URP).
- **Monetizare planificată:** Free-to-Play cu DLC ("Supporter Pack" - cosmetice, claxoane, biciclete speciale) sau preț mic indie (2-5 EUR).
- **Limba jocului:** Română (replici, interfață, umor local).

---

## 2. Direcție Vizuală și Estetică (Vezi `concept_gameplay.png`)
- **Stil grafic:** 3D Cel-Shaded / Toon Shader cu contur negru pronunțat (Outline), inspirat din *Borderlands* / *Hi-Fi Rush* / *Untitled Goose Game*.
- **Decor:** Arhitectură urbană din București (blocuri comuniste cu aparate de aer condiționat, chioșcuri, stâlpișori anti-parcare gri, piste verzi de biciclete blocate, mașini parcate pe trotuar cu avariile pornite).
- **Personaj Principal:** Biciclist cu cască, cameră de acțiune montată pe cască, ochelari de soare și vestă reflectorizantă galben-verde.
- **Interfață (HUD / UI):**
  - **Stânga sus:** Indicator tip cameră de acțiune (`● REC 00:14`, iconiță baterie, colțuri de încadrare alb-negru pe tot ecranul).
  - **Centru sus:** Obiectivul activ într-o casetă semi-transparentă (ex: `ELIBEREAZĂ TROTUARUL`).
  - **Dreapta sus:** `TENSION METER` (bară progresivă de la verde la roșu cu iconiță expresivă care arată nivelul de nervi al șoferului/cartierului).
  - **Stânga jos:** Minimap circular cu străzi, direcția jucătorului și semne de exclamare roșii (`!`) pentru mașinile parcate ilegal.
  - **Centru jos:** Caseta de subtitrări stil bandă desenată (ex: `[BroRider]: "Bună ziua! Avaria nu este loc de parcare."`).
  - **Context Action (în lume):** Prompt flotant lângă țintă (ex: `[E] SUNĂ LA POLIȚIA LOCALĂ`).

---

## 3. Psihologia și Comportamentul Personajului (State Machine)
Personajul nu acționează haotic, ci urmează o escaladare realist-satirică în 4 stări distincte (care vor fi rafinate ulterior din fișierul `PERSONA.md`):
1. **Starea 1 - Observatorul Calm (Patrulare):** Merge pe bicicletă, comentează relaxat și ironic despre starea pistelor, salută alți bicicliști și pietoni.
2. **Starea 2 - Abordarea Civilizată (Confruntare ușoară):** Detectează o mașină pe trotuar/pistă cu avariile pornite. Se oprește, folosește formule politicoase dar tăioase (*"Bună ziua, aveți o problemă tehnică sau doar la parcare?"*).
3. **Starea 3 - Citarea Legii (Escaladare):** Dacă șoferul devine arogant/agresiv, personajul activează modul "Filmare Sesizare" (efect ușor fisheye/GoPro, recitare articole din Codul Rutier OUG 195/2002) fără să cedeze teren.
4. **Starea 4 - Apelul la Autorități (Finalizare):** Apăsarea tastei `[E]` declanșează apelul la Poliția Locală / Brigada Rutieră. După un timer, apare o sirenă în depărtare, iar mașina este fie ridicată comedic de o macara, fie pleacă în trombă.

---

## 4. Arhetipuri de NPC-uri și Mecanici de Haos
- **Șoferul Grăbit / Nervos:** Claxonează agresiv, crește rapid `Tension Meter`-ul, iese din mașină gesticulând sau aruncă cu obiecte ușoare (fizică ragdoll/arcade) la 100% tensiune.
- **Șoferul Calm / Speriat:** Spune *"Gata, șefu, mut acum"* și pleacă rapid când vede camera.
- **Pietonul Susținător:** Aplaudă când se eliberează trotuarul și oferă bonus de Moral / Scor.
- **Interacțiuni cu orașul:** Montare de stâlpișori anti-parcare cu efecte de praf, scântei și screen-shake; folosirea soneriei de bicicletă (`Space`) pentru a speria pietonii care merg pe pista verde.

---

## 5. Sistemul Audio (Voice Acting Custom & Haos Ambiental)
- **Voci:** Replicile vor fi înregistrate manual de dezvoltator (fișiere `.wav` în `Assets/Audio/Hero/` și `Assets/Audio/Drivers/`).
- **Reguli Audio în Unity:**
  - Aplică variație aleatorie subtilă de pitch (`Random.Range(0.92f, 1.08f)`) pe replicile NPC-urilor pentru diversitate.
  - Aplică un filtru **Low-Pass** pe vocea șoferului când are geamul mașinii ridicat, care se dezactivează lin când coboară geamul.
  - **AmbientTrafficAudio:** Cu cât se blochează mai multe mașini în spatele jucătorului, cu atât crește frecvența claxoanelor, a motoarelor turate și a muzicii în surdină din mașini.

---

## 6. Reguli Tehnice și de Dezvoltare pentru Claude Code
1. **Modularitate:** Scrie cod C# curat, decuplat și bine comentat pentru Unity 6, expunând variabilele cheie (`[SerializeField]`) în Inspector pentru ajustare rapidă.
2. **Game Feel Obligatoriu:** Orice mecanică nouă implementată trebuie să includă simultan:
   - Feedback vizual (animație, particule, screen shake sau schimbare de FOV);
   - Declanșator audio (efect sonor sau replică);
   - Reacție din partea NPC-urilor din proximitate.
3. **Optimizare Tokeni & Context:** Lucrează pe sisteme izolate (ex: întâi Controller-ul de Bicicletă, apoi Sistemul de Interacțiune/Sesizare, apoi UI-ul). Păstrează arhitectura simplă și ușor de testat într-o scenă sandbox.




Calendar estimativ de dezvoltare (pas cu pas)
• Săptămâna 1: Setup & Prototipul de bază (Core Loop)
• Instalarea Unity 6, conectarea Claude Code prin Unity MCP și importarea unui pachet gratuit de oraș low-poly + bicicletă.
• Programarea controlului bicicletei, a camerei (inclusiv modul GoPro) și a Shader-ului Toon (conturul negru).
• Săptămânile 2 – 3: Mecanicile de haos și AI-ul șoferilor
• Crearea sistemului de mașini parcate pe avarii, montarea stâlpișorilor, apelul la Poliția Locală (macaraua care ridică mașina) și Tension Meter-ul.
• Programarea celor 3 tipuri de șoferi și a pietonilor.
• Săptămâna 4: Audio, Voci și Interfață (UI)
• Înregistrarea replicilor cu vocea ta, aplicarea efectelor (pitch, filtru de geam închis/deschis) și adăugarea claxoanelor și a soneriei.
• Finalizarea HUD-ului din concept_gameplay.png (minimap, bara de obiectiv, subtitrări).
• Săptămânile 5 – 6: Designul nivelurilor, Bug-fixing și Pregătirea pentru Steam
• Construirea celor 4–5 scenarii/cartiere (ex: Bulevardul Magheru, Piața Unirii, Străduță de cartier la oră de vârf).
• Testare intensă (rezolvarea bug-urilor de fizică), crearea paginii de Steam (Steamworks cere ca pagina Coming Soon să fie publică cu cel puțin 2 săptămâni înainte de lansare) și trimiterea cheilor către streameri.



Ce îți poate lungi sau scurta cel mai mult timpul
• Ce scurtează timpul la jumătate: Să folosești modele 3D gata făcute (de pe Unity Asset Store sau Kenney.nl) pentru clădiri, mașini și oameni, lăsându-l pe Claude Code să se ocupe doar de cod, fizică și interfață.
Ce lungeste cel mai mult timpul: Să încerci să faci animații complexe de la zero sau să adaugi prea multe mecanici complicate (ex: trafic realist ca în GTA în loc de trafic arcade simplu).
