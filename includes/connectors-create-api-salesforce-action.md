Teraz, dodano warunek jego coś interesującego przy użyciu danych hello jest generowany przez wyzwalacz hello toodo czasu. Wykonaj te kroki hello tooadd **Salesforce - Get obiektu** akcji. Ta akcja otrzyma danych hello każdym razem, gdy jest tworzony nowy potencjalnych klientów. Zostanie również Dodaj drugą akcję korzystające z danych hello z hello Salesforce - Get toosend Akcja obiektu poczty e-mail przy użyciu łącznika hello usługi Office 365.  

Ta akcja hello tooconfigure, konieczne będzie hello tooprovide następujących informacji. Można zauważyć jest łatwe toouse danych wygenerowane przez wyzwalacz hello jako dane wejściowe dla niektórych właściwości hello hello nowy plik:

| Utwórz właściwość pliku | Opis |
| --- | --- |
| Typ obiektu |To typ hello obiektu Salesforce, które planuje się. Przykłady są realizacji, kont itd. |
| Identyfikator obiektu: |Reprezentuje identyfikator dla obiekt hello. |

1. Wybierz **Dodaj akcję** łącza. To pole wyszukiwania hello otwiera gdzie możesz wyszukać dowolną akcję należy chcieliby tootake. Na przykład Salesforce akcje są przydatne.      
   ![Obraz akcji SalesForce 1](./media/connectors-create-api-salesforce/action-1.png)  
2. Wprowadź *salesforce* toosearch dla toosalesforce powiązanych działań.
3. Wybierz **Salesforce - Get obiektu** jako hello tootake akcji.   **Uwaga**: użytkownik będzie zostanie wyświetlony monit o tooauthorize tooaccess aplikacji logiki, Twoje konto Salesforce, jeśli nie zostało zrobione to wcześniej.    
   ![Obraz akcji SalesForce 2](./media/connectors-create-api-salesforce/action-2.png)    
4. Witaj **obiektu Get** sterowania zostanie otwarta.  
5. Wybierz *prowadzić* jako typ obiektu hello.
6. Wybierz hello **obiektu o identyfikatorze** formantu.
7. Wybierz **...**  tooexpand hello listy tokenów, które mogą służyć jako dane wejściowe dla akcji.       
   ![Obraz akcji SalesForce 3](./media/connectors-create-api-salesforce/action-3.png)    
8. Wybierz **prowadzić identyfikator** sterowania zostanie otwarta.   
   ![Obraz akcji SalesForce 4](./media/connectors-create-api-salesforce/action-4.png)     
9. Należy zauważyć, że token prowadzić identyfikator hello znajduje się teraz w hello kontroli Identyfikatora obiektu, wskazującą, że hello Get Akcja obiektu wyszuka realizacji o identyfikatorze, który jest równy toohello identyfikator realizacji potencjalnych klientów, która wyzwoliła tej aplikacji logiki.  
   ![Obraz akcji SalesForce 5](./media/connectors-create-api-salesforce/action-5.png)  
10. Zapisz swoją pracę. To wszystko, dodano hello Get obiektu akcji tooyour logiki aplikacji. Pobierz obiekt formantu powinna wyglądać następująco:    
    ![Obraz akcji SalesForce 6](./media/connectors-create-api-salesforce/action-6.png)  

Teraz, dodano tooget akcji potencjalnego klienta, możesz toodo coś interesującego z nowo utworzony hello realizacji. W przedsiębiorstwie może być toosend toonotify e-mail listę dystrybucyjną, że utworzono nowe realizacji. Użyjmy toosend łącznik usługi Office 365 hello wiadomość e-mail z niektórymi hello odpowiednich informacji z hello nowy obiekt potencjalnych klientów w usłudze Salesforce.  

1. Wybierz **Dodaj akcję** wprowadź *e-mail* hello wyszukiwania formantu. To filtruje hello toothose akcje, które są powiązane toosending i otrzymywania wiadomości e-mail.  
2. Wybierz hello **Office 365 Outlook - wysyłania usługi poczty e-mail** elementu listy. Jeśli nie utworzono już *połączenia* tooyour konto usługi Office 365, będzie można zostanie wyświetlony monit o tooenter toocreate poświadczeń użytkownika usługi Office 365 teraz. Po wykonaniu hello **wysłać wiadomość e-mail** sterowania zostanie otwarta.        
   ![Obraz akcji SalesForce 7](./media/connectors-create-api-salesforce/action-7.png)  
3. Wprowadź adres e-mail hello chcieliby hello tooin e-mail toosend **do** formantu.
4. W hello **podmiotu** kontrolować, wprowadź *nowe prowadzić utworzony* — a następnie wybierz pozycję hello *firmy* tokenu. Spowoduje to wyświetlenie hello *firmy* pola hello realizacji nowego utworzone w usłudze Salesforce.  
5. W hello **treści** można kontroli, wybierz dowolne tokeny powitania od hello nowy obiekt potencjalnych klientów i można również wprowadzić, niezależnie od tekstu, które chcesz toodisplay w treści hello hello poczty e-mail. Oto przykład:  
   ![Obraz akcji SalesForce 8](./media/connectors-create-api-salesforce/action-8.png)   
6. Zapisywanie przepływu pracy.  

To już wszystko. Aplikację logiki jest teraz ukończona.  

Teraz można przetestować aplikację logiki: w usłudze Salesforce, Utwórz nowe potencjalnego klienta, który spełnia warunek hello utworzony.  Po wykonaniu tego przewodnika w pełni, wystarczy utworzyć potencjalnego klienta adres e-mail, który zawiera *amazon.com* w nim. Po kilku sekundach powinno być wyzwalane aplikację logiki i wyniki hello może wyglądać podobnie toothis:  
![Obraz akcji SalesForce 9](./media/connectors-create-api-salesforce/action-9.png)  

