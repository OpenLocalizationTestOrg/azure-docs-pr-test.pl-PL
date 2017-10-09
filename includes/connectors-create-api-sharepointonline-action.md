Teraz, dodano wyzwalacz jego coś interesującego przy użyciu danych hello jest generowany przez wyzwalacz hello toodo czasu. Wykonaj te kroki hello tooadd **usługi SharePoint Online — Utwórz plik** akcji. Ta akcja spowoduje utworzenie pliku w usłudze SharePoint Online każdej czasu hello nowego elementu wyzwalacza uruchamiany. 

Ta akcja hello tooconfigure, konieczne będzie hello tooprovide następujących informacji. Użytkownik poda te informacje, można zauważyć jest łatwe toouse danych wygenerowane przez wyzwalacz hello jako dane wejściowe dla niektórych właściwości hello hello nowy plik:

| Utwórz właściwość pliku | Opis |
| --- | --- |
| Adres URL witryny |To jest adres URL hello hello witryny usługi SharePoint Online, w którym ma toocreate hello nowy plik. Wybierz lokację hello z listy hello przedstawiony. |
| Ścieżka folderu |To jest hello folder (adres URL witryny wybrane w poprzednim kroku hello hello) rozmieszczenia hello nowy plik. Wyszukaj i wybierz hello folder. |
| Nazwa pliku |To jest nazwa hello tworzony plik hello. |
| Zawartość pliku |zawartość Hello, który zostanie zapisany plik toohello. |

1. Wybierz **+ nowy krok** tooadd hello akcji.  
   ![Obraz akcji online programu SharePoint 1](./media/connectors-create-api-sharepointonline/action-1.png)  
2. Wybierz hello **Dodaj akcję** łącza. To pole wyszukiwania hello otwiera gdzie możesz wyszukać dowolną akcję należy chcieliby tootake. Na przykład SharePoint akcje są przydatne.    
   ![Obraz akcji online programu SharePoint 2](./media/connectors-create-api-sharepointonline/action-2.png)    
3. Wprowadź *sharepoint* toosearch dla tooSharePoint powiązanych działań.
4. Wybierz **usługi SharePoint Online — Utwórz plik** jako hello tootake akcji.   **Uwaga**: użytkownik będzie zostanie wyświetlony monit o tooauthorize Twojego tooaccess aplikacji logiki konta programu SharePoint, jeśli wcześniej nie został utworzony tooSharePoint połączenia w trybie Online.    
   ![Obraz akcji online programu SharePoint 3](./media/connectors-create-api-sharepointonline/action-3.png)    
5. Witaj **Utwórz plik** sterowania zostanie otwarta.   
   ![Obraz akcji online programu SharePoint 4](./media/connectors-create-api-sharepointonline/action-4.png)     
6. Wybierz **adres URL witryny** i przeglądania toofind hello lokacji, gdzie chcesz toocreate hello pliku.     
   ![Obraz akcji online programu SharePoint 5](./media/connectors-create-api-sharepointonline/action-5.png)  
7. Wybierz **ścieżka folderu** i folderu hello toofind przeglądania rozmieszczenia hello nowy plik.  
   ![Obraz akcji online programu SharePoint 6](./media/connectors-create-api-sharepointonline/action-6.png)  
8. Wybierz hello **nazwę pliku** kontroli i wprowadź nazwę hello pliku hello ma toocreate. W tym miejscu można wprowadzić nazwę pliku hello bezpośrednio lub można użyć dowolnego z właściwości hello z wyzwalacza hello, utworzonej wcześniej. Aby to zrobić, wybierając właściwości z listy hello **dane wyjściowe z podczas tworzenia nowego elementu**. Ta lista jest wyświetlana tylko po wybraniu hello **nazwę pliku** formantu. W tym walkthough wybrano ID (identyfikator hello hello nowy element listy) jako hello nazwy pliku hello tworzonego przez hello **usługi SharePoint Online — Utwórz plik** akcji.    
   ![Obraz akcji online programu SharePoint 7](./media/connectors-create-api-sharepointonline/action-7.png)  
9. Wybierz hello **plików zawartości** kontroli i wprowadź hello zawartości, który zostanie zapisany plik toohello, który zostanie utworzony. Hello zawartości pliku Zwróć uwagę, że można użyć dowolnego z właściwości hello z wyzwalacza hello, utworzonej wcześniej. Po prostu wybierz hello właściwości z listy hello przedstawiony. Alternatywnie można wprowadzić hello **plików zawartości** tekst bezpośrednio w formancie hello. W tym przykładzie I wybrane niektórych właściwości i dodać spacje i łącznika między każdej właściwości.        
   ![Obraz akcji online programu SharePoint 8](./media/connectors-create-api-sharepointonline/action-8.png)  
10. Zapisywanie przepływu pracy tooyour zmiany hello  
11. Gratulacje, masz teraz aplikacji logiki funkcjonalnej wyzwalana po dodaniu nowego elementu tooa listy programu SharePoint Online. Aplikacja Hello spowoduje to utworzenie pliku przy użyciu właściwości hello z hello nowy element listy.  Teraz możesz przetestować go przez utworzenie nowego elementu hello listy programu SharePoint. 

