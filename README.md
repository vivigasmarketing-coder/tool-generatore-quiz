# Come utilizzare il tool?
Inizia scrivento main nella url https://vivigasmarketing-coder.github.io/tool-generatore-quiz/main
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
