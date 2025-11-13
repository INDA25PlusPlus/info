# Uppgift 9 - Kryptografi

## Uppgifter

Skapa ett repo i ++ organizationen som heter **kth-id**-cryptography där ni lägger all kod.

Läxan är att utveckla ett enkelt krypterat remote fillagringssystem i grupper av 2. Vi vill ha följande features:

- En klient och en server som pratar över nätverk
- Servern ska lagra godtyckliga par av (filid, fildata) (i RAM om ni är lata, och enklast med filid:n som är små heltal)
- All data ska krypteras av klienten innan den skickas till servern, med en nyckel härledd från ett lösenord och en slumpmässig nonce per kryptering\*
- Datan ska även vara signerad med samma nyckel och med fil-id:t, så att servern inte kan byta ut den mot annan slumpmässig data/en annan fil\*\*
- Vi vill kunna verifiera att data faktiskt lagrats/finns tillgänglig, och är up-to-date (servern ska inte kunna ge oss gamla resultat)

\* Vi vill inte att det ska avslöjas om vi krypterar samma fil två gånger.

\*\* Potentiell attack om vi inte gör detta: säg att det är backuper vi lagrar, och en ond server byter ut en fil som körs vid startup mot malign kod från webbläsarcachen. Accessmönster skulle kunna användas för att ta reda på var dessa filer finns lagrade, utan att faktiskt behöva dekryptera dem.

Den sistnämnda punkten är antagligen den mest intressanta. Ett sätt vi skulle kunna göra det på är att låta klienten spara den senaste hashen av alla lagrade filer, och då och då begära ut slumpmässiga filer och se att deras hashar överensstämmer. Det kräver dock att vi lagrar en hash för varje fil, vilket tar för mycket minne -- vi skulle helst vilja ha en klient som bara lagrar en konstant mängd data. För att komma runt detta använder vi oss av hashar av hashar, i form av ett [Merkle-träd](https://en.wikipedia.org/wiki/Merkle_tree).

Sättet det fungerar på att är vi placerar ut filerna som lövnoder i ett binärt träd på servern, lagrar `h[x] = H(x.data)` för dem för något lämpligt val av hashfunktion H, och för alla icke-lövnoder lagrar `h[x] = H(h[x.left] + h[x.right])`. Vi kan därefter använda `h[rotnod]` som en hash av hela trädet, som lagras lokalt på klienten. När vi frågar om en fils data kan servern ge tillbaka den datan tillsammans med komplementerande hashar uppåt i trädet, som tillåter klienten att verifiera att hashen av hela trädet är korrekt ([illustration](https://i.imgur.com/6c5HsdB.png)). Skrivningar kan göras på motsvarande sätt: servern skickar över komplementerande hashar som klienten kan verifiera och använda för att uppdatera sin lokala rotnodshash. Eftersom vi har ett välbalancerat binärt träd krävs bara att ett logaritmiskt antal hashar skickas över/uppdateras i varje steg.

Det är lite överlapp i funktion mellan Merkleträdet och punkt 4 (signering av filer) -- båda verifierar att filer är korrekta. För att undvika upprepat arbete skulle man kunna skippa punkt 4, eller låta `h[x] = x.signatur` för lövnoderna.

Ni får själva avgöra vilka krypterings-, signerings- och hashningsalgoritmer som är lämpliga. Beskriv valen lite kort i er README.

Ni har full frihet i detaljerna kring systemet, t.ex. programmeringsspråk, hur ni gör klient-server-kommunikation, o.s.v. En detalj som är värd att nämna är fil-id:na -- för att göra saker enkelt kan det vara rimligt att låta dem vara tal mellan 0 och 2^n-1 för något litet fixerat tal n, så att vi får perfekta binära träd. Om ni däremot vill låta dem vara godtyckligt stora tal eller hashar av filnamn och få lata eller självbalancerande träd, go for it. Se längre ner för lite roliga möjliga vidareutvecklingar.

---

En steg-för-steg-beskrivning, ifall det hjälper att utgå från:
- Sätt upp server/klient som kan prata med varandra över valfritt protokoll (HTTP, TCP, gRPC, Cap'n'proto, ...). Ni kan t.ex. kopiera kod från de nätverkade schacken för detta.
- Börja med att låta servern lagra allting i RAM, få den att kunna läsa/skriva godtycklig data baserat på vad klienten skickar
- Skriv en klient som krypterar/signerar/dekrypterar/verifierar data och kommunicerar med servern. Testa att allt funkar.
- Börja implementera Merkle-träd i servern. Om ni vill kan ni ha en init-signal, som när den tas emot konstruerar datastrukturen. Ursprungsdatan kan du låta vara något godtyckligt nonsens som klienten inte kan dekryptera, eller någon slags specialrepresentation för "ingenting". Skicka tillbaka topp-hashen till klienten.
- Lägg till läsning av filer med Merkleträdsverifiering på server/klient. Testa att klientens topp-hash stämmer överens med serverns.
- Lägg till skrivning av filer. Samma verifiering som för läsning, men servern och klienten uppdaterar även sina hashar, och klienten lagrar topp-hashen.

### Utökningar

- Som beskrivet har servern inget som helst sätt att veta att det är rätt klient som pratar med den. Så medan klienten enligt protokollet ovan kan känna sig säker på att dess data inte kan läsas av andra, och kan *upptäcka* om den modifieras, finns det inget som faktiskt förhindrar den från att modifieras (förstöras) av andra. Det kan därmed vara värt att lägga till någon slags klient-authentisering till servern. Förutom förstörd data kan ett lager av skydd på servern även tillåta oss att rate-limita bruteforce av klientnyckeln. Kan göras med antingen manuell symmetrisk krypto, och/eller HTTPS om man är lat.
- Att fil-id:n begränsas till små heltal är inte helt idealiskt -- det hade varit mycket trevligare om de hade kunnat sättas lika med hashar eller krypteringar av filnamn. Detta komplicerar dock Merkle-trädet: om fil-id:na var t.ex. 80 bitar långa skulle ett komplett binärt träd ha storlek 2^80 (~ 10^27), vilket inte går att lagra. Jag tänker mig spontant tre sätt man skulle kunna komma runt det här på:
    - man skulle kunna tänka på fillagringssystemet som en hashtabell, sätta storleken dynamiskt på något smart sätt, och hantera kollisioner på något annat smart sätt (säg [cuckoo hashing](https://en.wikipedia.org/wiki/Cuckoo_hashing))
    - man skulle kunna använda ett självbalancerande träd (t.ex. en [treap](https://en.wikipedia.org/wiki/Treap)) i stället för ett komplett binärt träd. Möjligen aningen komplext att skickar över information om ombalanceringar till klienten.
    - (enklast) man skulle kunna låta noder vara "lata" och materialisera dem när det behövs, och annars säga att de har `h[x] = 0`
- Det hade varit nice om man kunnat läsa/skriva datan från flera enheter. Detta förstör dock vår förmåga att hela tiden lagra den senaste topp-hashen på klienten för att se att servern inte fuskar med sin fillagring... Nånting vi skulle kunna göra är att lagra signerade topphashar på servern, vilket hjälper en aning -- dock kan servern fortfarande godtyckligt reverta tillbaka till gamla versioner av filer, och låtsas som att de kom från någon annan enhet. Vi skulle kunna signera även ett timestamp, vilket hjälper desto mer -- dock kan servern fortfarande hålla flera forks av datan, t.ex. en per enhet, och hoppa mellan dem vid läsningar halvt godtyckligt. Det kräver även att vi har synkroniserade klockor. En sista idé är att signera topp-hashar, och lagra dem i ett till Merkle-träd, som bara skrivs vänster->höger. Klienter kan då verifiera att deras senaste topp-hash är till vänster om den senast lagrade och fast-forwarda den. Både Bitcoin och Git gör i princip det här.

### Material

- Merkleträd: [https://en.wikipedia.org/wiki/Merkle_tree](https://en.wikipedia.org/wiki/Merkle_tree), [https://www.codeproject.com/articles/Understanding-Merkle-Trees-Why-Use-Them-Who-Uses-T](https://www.codeproject.com/articles/Understanding-Merkle-Trees-Why-Use-Them-Who-Uses-T), Google (visserligen för att det mesta man googlar fram verkar handla om hur Merkleträd används i bitcoin...)
- [https://www.tarsnap.com/](https://www.tarsnap.com/) gör något ganska motsvarande det här, kan vara värt att läsa på om.
- Användningen av Merkleträd i Roughtime för snabba asymmetriska signaturer: [https://roughtime.googlesource.com/roughtime](https://roughtime.googlesource.com/roughtime)

Kryptobibliotek:
- C/C++: [libsodium](https://download.libsodium.org/doc/) är bra. Crypto++. OpenSSL/BoringSSL för HTTPS.
- Java: [kalium](https://github.com/abstractj/kalium) för NaCl-bindings, annars javax.crypto (som utökas av Bouncy Castle för fler algoritmer). Det API:et är dock väldigt generiskt och försöker täcka in *allt*, vilket gör det lätt att skjuta sig själv i foten. Det finns t.ex. stöd för RC4, ECB, NULL-chiffer (!), helt utan varningar i dokumentationen...
- Rust: [ring](https://github.com/briansmith/ring), [rust-crypto](https://github.com/DaGenix/rust-crypto), [rustls](https://github.com/ctz/rustls).
- Go: [crypto](https://golang.org/pkg/crypto/), [http](https://golang.org/pkg/net/http/) för HTTPS.
- Python: [cryptography](https://pypi.org/project/cryptography/).

För hashning brukar det flyta runt public domain single file-bibliotek på internet, som också är okej att använda (till skillnad från asymmetrisk krypto och AES är hashning svårt att felimplementera).

## Läsning

AEAD (authenticated encryption with associated data)
- [https://en.wikipedia.org/wiki/Authenticated_encryption](https://en.wikipedia.org/wiki/Authenticated_encryption)
- [https://www.imperialviolet.org/2015/05/16/aeads.html](https://www.imperialviolet.org/2015/05/16/aeads.html)

Kul läsning om kryptosårbarheter:
- [https://moxie.org/2011/12/13/the-cryptographic-doom-principle.html](https://moxie.org/2011/12/13/the-cryptographic-doom-principle.html)

Praktiska tips för om ni behöver göra krypto:
- AES-GCM och ChaCha20-Poly1305 båda rimliga val av AEADs om ni behöver kryptera något.
- SHA256 för generell hashning (alt. SHA512 med andra halvan av utdatan bortkapad för att undvika [length extension attacks](https://en.wikipedia.org/wiki/Length_extension_attack))
- Argon2 eller scrypt för lösenordshashning
- HTTPS för server-klient-kommunikation (gärna med fixerade certifikat)

[http://latacora.singles/2018/04/03/cryptographic-right-answers.html](http://latacora.singles/2018/04/03/cryptographic-right-answers.html) beskriver det här mer utförligt (motiveringar, fler sorter av kryptoprimitiver, och antagligen ännu bättre råd). https://download.libsodium.org/doc/ är biblioteket som frekvent refereras till däri (som gör det mesta rätt rent kryptomässigt, även om man sen kanske inte vill använda C-API:erna rakt av).

---

Det finns en hel del bra bloggar om krypto, ofta så som det utövas i praktiken:

- [https://www.imperialviolet.org/](https://www.imperialviolet.org/) Adam Langley, Googles/Chromes kryptoexpert. Bloggar sporadiskt nu för tiden, men arkivet är värt att gå igenom. Bra exempelbloggposter: [[1]](https://www.imperialviolet.org/2016/05/16/agility.html) [[2]](https://www.imperialviolet.org/2016/09/19/roughtime.html)
- [https://blog.cryptographyengineering.com/](https://blog.cryptographyengineering.com/) Matthew Green. Brukar ha nyheter om kryptoattacker med tekniska detaljer. Exempelbloggposter: [[1]](https://blog.cryptographyengineering.com/2013/02/15/why-i-hate-cbc-mac/) [[2]](https://blog.cryptographyengineering.com/2017/10/23/attack-of-the-week-duhk/) [[3]](https://blog.cryptographyengineering.com/2014/11/27/zero-knowledge-proofs-illustrated-primer/)
- [https://moxie.org/blog/](https://moxie.org/blog/) Moxie Marlinspike, skaparen av Signal. Bloggar sällan men har skrivit intressanta saker.
- [https://www.schneier.com/](https://www.schneier.com/) Bruce Shneier, allmän kryptokändis. Bloggar regelbundet, lite mycket politik för min smak egentligen.

Wikipedia-länkar:
- [HMAC](https://en.wikipedia.org/wiki/HMAC) (symmetrisk signering)
- [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) (notera speciellt sektionerna "Padding" och "Security and practical considerations")
- [One-time pad](https://en.wikipedia.org/wiki/One-time_pad) (det enda matematiskt säkra kryptosystemet, i praktiken ej använt)
- [Homomorphic encryption](https://en.wikipedia.org/wiki/Homomorphic_encryption) (beräkningar på data man inte kan läsa, superflashigt men inte så praktiskt)
- [Zero-knowledge proof](https://en.wikipedia.org/wiki/Zero-knowledge_proof) (mer på samma tema: metoder för att bevisa att man vet något, utan att behöva avslöja det)
- [Oblivious transfer](https://en.wikipedia.org/wiki/Oblivious_transfer) (ännu mer på samma tema: en metod för att be om data utan att någon vet vad man bett om)
- [Cryptographically secure pseudorandom number generator](https://en.wikipedia.org/wiki/Cryptographically_secure_pseudorandom_number_generator) (säkra slumpgeneratorer)
- [Timing attack](https://en.wikipedia.org/wiki/Timing_attack) (en attack mot kryptosystem som man kanske inte spontant tänker på. Paper om hur det kan se ut i praktiken: [http://v.wpi.edu/wp-content/uploads/Papers/Publications/seriously.pdf](http://v.wpi.edu/wp-content/uploads/Papers/Publications/seriously.pdf))

Finns bra böcker om krypto också ("crypto books" verkar ge vettiga träffar på Google), och kan rekommendera kursen DD2448 på KTH (går på våren, kräver möjligen diskmatte som förkunskap).
