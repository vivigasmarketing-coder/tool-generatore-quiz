# Come utilizzare il tool?
Per generare un nuovo quiz è possibile farlo da questo tool Generatore di Quiz Avanzato https://vivigasmarketing-coder.github.io/tool-generatore-quiz/main che consente di generarne di nuovi a più risposte e personalizzare colori, cta e testi in funzione della percentuale di risposte corrette.
Il tool consente di copiare i singoli quiz, generare codici univoci o generare un codice universale per l'import su instapage e associabile ad un referrer personalizzato.

Per l'import è sufficiente copiare il codice in allegato nella sezione dedicata del tool e si riavrà la situazione as-is.
Ogni volta conviene salvare il codice come avanzamento.
# Pubblicazione su Instapage #
#### I quiz sono tutti inseriti dentro un unica pagina in Instapage. ####
Si possono attivare i vari quiz modificando il referrer in query string:
- https://casa.vivienergia.it/quiz-vivienergyhub?referrer=caldaia
- https://casa.vivienergia.it/quiz-vivienergyhub?referrer=fotovoltaico
- https://casa.vivienergia.it/quiz-vivienergyhub?referrer=climatizzatore
- https://casa.vivienergia.it/quiz-vivienergyhub?referrer=wallbox
- https://casa.vivienergia.it/quiz-vivienergyhub?referrer=depuratore
- https://casa.vivienergia.it/quiz-vivienergyhub?referrer=greentips
- https://casa.vivienergia.it/quiz-vivienergyhub?referrer=telethon

# Tracciamenti
## Guida Rapida all'Inserimento dei Tracciamenti ##
I tracciamenti vanno inseriti nel file HTML all'interno del tag ```<script>``` che contiene tutta la logica di funzionamento del quiz. Nello specifico, vanno associati ai due pulsanti che vuoi monitorare: quello che avvia il quiz e quello finale che porta al sito.
### Tracciamento per il pulsante "Inizia il Quiz" ###
Questo codice serve a tracciare quando un utente clicca sul pulsante per avviare il quiz.
#### Dove inserirlo: ####
Cerca la funzione ```initializeQuiz()``` nel tuo codice. Il punto esatto è subito dopo la riga ```startBtn.addEventListener('click', startQuestions);.```
#### Codice da copiare ####
```
// ----- INSERISCI QUESTO CODICE PER IL PULSANTE 'START' -----
startBtn.addEventListener('click', function() {
    if (typeof tC !== 'undefined' && tC.event && typeof tC.event.quiz_veh === 'function') {
        tC.event.quiz_veh(this, {
            'tipo_quiz': quizConfig.referrer,
            'azione': 'start'
        });
    }
});
```

### Tracciamento per il pulsante finale (CTA) ###
Questo codice traccia i click sul pulsante finale che compare nella schermata dei risultati (es. "Scopri di più").
#### Dove inserirlo: ####
Cerca la funzione ```showResults()``` nel tuo codice. Il punto esatto è subito dopo la riga ```resultLinkEl.innerText = resultConfig.ctaText;```
#### Codice da copiare ####
```
// ----- INSERISCI QUESTO CODICE PER IL PULSANTE 'FINISH' -----
resultLinkEl.addEventListener('click', function() {
    if (typeof tC !== 'undefined' && tC.event && typeof tC.event.quiz_veh === 'function') {
        tC.event.quiz_veh(this, {
            'tipo_quiz': quizConfig.referrer,
            'azione': 'finish'
        });
    }
});
```
:bulb:In sintesi, stai semplicemente aggiungendo un nuovo "ascoltatore" (addEventListener) a ciascun pulsante per inviare l'evento di tracciamento specifico quando vengono cliccati. Il codice è già configurato per recuperare dinamicamente il tipo di quiz (quizConfig.referrer) e l'azione corretta (start o finish).
