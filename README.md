# Guida Hackathon

## Output richiesto

L'obbiettivo finale è la costruzione di un tool in grado di dialogare con il Chtabot di BTicino, comprendendo il più possibile le sue risposte e sfruttandole per ottenere il maggior numero di informazioni possibili sulla nuova linea di prodotti Living Now.
Il chatbot oltre a rispondere alle domande inviategli, può dare dei suggerimenti o insights per proseguire la conversazione. Può restituire infatti domande aggiuntive con un elenco di risposte chiuse, rispondendo alle quali è possibile ottenere informazioni in più sui prodotti.
Ai fini della valutazione dei risultati, è richiesto che il tool consegnato produca, una volta eseguito, un output testuale (file txt o similari) o un prompt, contenente la conversazione completa avvenuta con il chatbot.
Il tool eseguibile dovrà essere contenuto in un archivio Zip, contenente tutti i file necessari all'esecuzione, oltre che a istruzioni su come eseguirlo e quali dipendenze installare, nel caso in cui si adottino soluzioni che comprendono terze parti.
Sarà oggetto di valutazione anche la soluzione tecnica utilizzata, per questo verrà richiesta una presentazione di come si è arrivati ad ottenere il risultato.

## Come comunicare con il Chatbot

I motori del chatbot sono raggiungibili tramite delle API fornite dagli organizzatori.
Le API memorizzano il contesto della conversazione, in modo tale da ottenere un flusso di messaggi correlati tra di loro. Es: se si chiedono informazioni sul prodotto 'X', le successive domande saranno riferite al prodotto 'X' se si omette di specificarlo nei messaggi successivi.
Sarà possibile in qualsiasi momento resettare la conversazione e ricominciarne una nuova utilizzando il messaggio "reset".

### Documentazione API

Per comunicare con l'API si effettueranno chiamate HTTP nel seguente modo:
``` 
POST 'https://bthack.azurewebsites.net/home'
--header 'Content-Type: application/json'
--body 
  {
    "TeamId": "ID del team fornito",
    "ChatMessage": "Ciao"
  }
```
Bisogna quindi passare un Body di tipo JSON contenente il TeamID, che è l'id del team fornitovi dagli organizzatori, e il ChatMessage, che è il messaggio che si vuole mandare al chatbot.
Si otterrà quindi una risposta nel seguente formato:
```
  {
    "teamId": "TeamID",
    "chatMessage": "Ciao",
    "chatResponse": " Ciao 😊",
    "chatResponseQuestion": null,
    "chatResponseOptions": null
  }
```
E nel caso in cui il chatbot voglia aggiungere dei suggerimenti per proseguire con la conversazione, si avrà una risposta così strutturata:
```
{
    "teamId": "TeamID",
    "chatMessage": "bene grazie! Ma cosa sono gli scenari?",
    "chatResponse": " Con Living Now vengono forniti quattro scenari di base nella App: lo spegnimento generale, l'accensione generale, il risveglio e la notte. Tramite l' app è sempre possibile configurare e modificare i singoli dispositivi che sono compresi negli scenari",
    "chatResponseQuestion": "Vuoi scoprire tutte le potenzialità dell'applicazione Home+Control?",
    "chatResponseOptions": [
        "Sì",
        "No"
    ]
}
```
I primi 2 campi sono gli stessi che ha ricevuto nella richiesta API, mentre i successivi sono aggiunti dal chatbot e costituiscono rispettivamente la risposta alla domanda, un suggerimento da parte del chatbot, e le possibili risposte al suggerimento stesso.
Una delle "chatResponseOptions" può essere utilizzata per proseguire la conversazione e ricavare ulteriori informazioni senza che sia conteggiata come domanda fatta al chatbot ai fini della valutazione.
