Scanner Documenti Formato Tessera

Una web application client-side avanzata, sviluppata da Spina Michele, progettata per acquisire, riconoscere, ritagliare, raddrizzare e impaginare documenti d'identità in formato tessera (formato ID-1, es. carte d'identità, patenti, tessere sanitarie) direttamente all'interno del browser, senza la necessità di installare software aggiuntivi o inviare dati a server esterni.

🚀 Panoramica del Progetto e Funzionalità Principali

L'applicazione trasforma qualsiasi fotocamera di uno smartphone o webcam in uno scanner professionale per documenti tessere. Tra le sue caratteristiche principali:

Rilevamento e Raddrizzamento Automatico (OpenCV.js): Grazie alla visione artificiale, il sistema individua automaticamente i bordi del documento nello spazio, applicando una trasformazione prospettica (perspective warp) per estrarre la tessera perfettamente inquadrata.

Bordi Arrotondati Standard ISO/IEC 7810: Ciascuna tessera estratta viene rifinita con gli angoli arrotondati conformi agli standard internazionali per i documenti d'identità (raggio di 3.18 mm).

Gestione Multi-Tessera Dinamica: È possibile aggiungere fino a 12 tessere per sessione, gestendo in modo indipendente il Fronte e il Retro di ciascuna.

Controllo Qualità Integrato: Il sistema esegue controlli automatici su ogni scatto per verificare la nitidezza (rilevamento sfocatura tramite operatore di Laplace) e i livelli corretti di luminosità (blocco di immagini troppo buie o con riflessi eccessivi).

Anteprima PDF Interattiva: Un modale integrato con visualizzatore PDF permette di controllare il risultato finale prima del download definitivo.

Esportazione in Formato A4 (8 Tessere per Pagina): Generazione automatica di un documento PDF in formato A4, organizzato in una griglia ordinata di 4 righe e 2 colonne (fronte e retro appaiati sulla stessa riga).

Persistenza della Sessione: Salvataggio automatico dello stato tramite sessionStorage, che previene la perdita dei dati in caso di rinvii accidentali della pagina.

🛠 Requisiti Tecnici e Librerie Esterne

Trattandosi di un'applicazione basata interamente sul browser (Client-Side Pure), non richiede alcun backend o server di elaborazione.

Librerie esterne (caricate tramite CDN):

OpenCV.js (v4.8.0): Motore di elaborazione di visione artificiale e manipolazione matriciale.

jsPDF (v2.5.1): Libreria per la generazione e manipolazione di file PDF direttamente in JavaScript.

Requisiti di Sistema:

Un browser moderno abilitato a JavaScript e WebAssembly (Chrome, Edge, Firefox, Safari).

Dispositivo dotato di fotocamera (consigliato smartphone o tablet) o accesso a file di immagini locali.

📖 Guida all'Utilizzo

Avvio dell'Applicazione: Apri il file Scanid.html nel browser. Attendi qualche secondo che il motore OpenCV.js si inizializzi (lo stato passerà a "Scanner pronto").

Aggiunta Tessere: L'applicazione parte con una tessera predefinita. Puoi cliccare su "+ Aggiungi tessera" per inserirne di nuove (fino a un massimo di 12).

Acquisizione Fronte / Retro:

Clicca su "Scatta / Carica" nel riquadro del Fronte o del Retro.

Su dispositivi mobili si aprirà direttamente la fotocamera; su desktop potrai selezionare un'immagine dal disco.

Il sistema analizzerà l'immagine, la ritaglierà e mostrerà l'anteprima solo se i parametri di qualità sono soddisfatti.

Modifica o Annullamento: In caso di scatto non ottimale, puoi cliccare su "Annulla" all'interno dello slot per ripetere l'operazione, oppure su "✕ Rimuovi" per eliminare l'intera tessera.

Anteprima PDF: Una volta completati tutti i lati di tutte le tessere, si attiverà il pulsante "Anteprima PDF". Cliccandoci potrai visualizzare l'impaginazione in tempo reale.

Esportazione PDF: Inserisci il nome desiderato per il file nell'apposito campo e clicca su "Esporta PDF (A4 - 8 tessere per pagina)". Il sistema salverà il documento (sfruttando le API di salvataggio avanzate del browser, se supportate).

💡 Consigli per un Corretto Scatto Fotografico

Per garantire il corretto riconoscimento automatico dei bordi da parte di OpenCV, segui queste best practice:

Sfondo Contrastato: Posiziona la tessera su uno sfondo scuro e uniforme (es. un tavolo scuro o un foglio nero) se la tessera è chiara, o viceversa. Evita sfondi confusi o simili al colore della tessera.

Luce Uniforme: Assicurati che l'ambiente sia ben illuminato. Evita ombre marcate sul documento o riflessi speculari forti (specialmente su tessere plastificate).

Margini Visibili: Lascia un piccolo bordo di sfondo attorno alla tessera durante lo scatto; evita di tagliare i bordi fuori dall'inquadratura.

Fotocamera Parallela: Inquadra il documento dall'alto mantenendo il telefono o la fotocamera il più possibile paralleli alla superficie della tessera.

💾 Gestione dello Stato e Persistenza (sessionStorage)

L'applicazione memorizza automaticamente lo stato corrente della sessione all'interno del sessionStorage del browser (scanner_tessere_state_v2).
Questo significa che:

Se ricarichi inavvertitamente la pagina o chiudi il modal, le immagini elaborate e i dati inseriti non andranno persi.

Lo stato viene pulito o aggiornato dinamicamente a ogni modifica, aggiunta o reset dei singoli slot.
