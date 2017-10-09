Teraz, dodano wyzwalacz jego coś interesującego przy użyciu danych hello jest generowany przez wyzwalacz hello toodo czasu. Wykonaj te kroki tooadd hello **SFTP — folder wyodrębniania** akcji. Ta akcja wyodrębnia hello zawartości pliku po spełnieniu warunków hello zdefiniowane. 

Ta akcja hello tooconfigure, konieczne będzie hello tooprovide następujących informacji. Można zauważyć jest łatwe toouse danych wygenerowane przez wyzwalacz hello jako dane wejściowe dla niektórych właściwości hello hello nowy plik:

| SFTP - extract właściwości folderu | Opis |
| --- | --- |
| Ścieżka pliku archiwum źródła |To jest ścieżka hello pliku hello wyodrębniania. Możesz wybrać jedną z tokenów hello z wcześniejszych akcji lub przeglądać ścieżka pliku hello toofind hello SFTP serwera. |
| Ścieżka folderu docelowego |To jest ścieżka hello rozmieszczenia hello wyodrębnione pliki. Można wybrać jednego z tokenów hello z wcześniejszych akcji jako ścieżkę docelową hello lub serwera SFTP hello Przeglądaj i wybierz ścieżkę. |
| Czy zastąpić? |Wskazuje, czy plik o hello sama nazwa zgodnie z hello wyodrębnionego pliku znajduje się w ścieżka folderu docelowego hello, jeśli powinien można zastąpić istniejącego pliku hello, lub nie. |

Rozpocznijmy Dodawanie hello akcji tooextract hello plików, gdy warunek hello zdefiniowanego wcześniej nie jest zbyt*True*. 

1. Wybierz **Dodaj akcję**.        
   ![Obraz warunku akcji SFTP 6](./media/connectors-create-api-sftp/condition-6.png)   
2. Wybierz hello **SFTP — folder wyodrębniania** akcji      
   ![Obraz warunku akcji SFTP 7](./media/connectors-create-api-sftp/condition-7.png)   
3. Wybierz **ścieżki pliku źródłowego archiwum**              
   ![Obraz warunku akcji SFTP 9](./media/connectors-create-api-sftp/condition-9.png)   
4. Wybierz hello **ścieżka pliku** tokenu. To ustawienie określa użyje hello ścieżka pliku hello, który hello znaleziono jako ścieżka pliku archiwum źródła hello wyzwalacza.           
   ![Obraz warunku akcji SFTP 10](./media/connectors-create-api-sftp/condition-10.png)   
5. Wybierz **ścieżkę folderu docelowego**           
   ![Obraz warunku akcji SFTP 11](./media/connectors-create-api-sftp/condition-11.png)   
6. Wybierz hello **ścieżka pliku** tokenu. To ustawienie określa użyje hello ścieżka pliku hello, który hello wyzwalacza znaleziono jako ścieżkę docelową hello hello wyodrębnione pliki.   
7. Wprowadź *\ExtractedFile* w hello **ścieżkę folderu docelowego** formantu. W tym zaraz po token ścieżka pliku hello w hello kontroli ścieżka folderu docelowego.         
   ![Obraz warunku akcji SFTP 12](./media/connectors-create-api-sftp/condition-12.png)   
8. Wprowadź *True* w hello **Zastąp?* tooindicate formant, który powinien być zastąpione istniejące pliki, jeśli mają takie same nazwy jako hello hello wyodrębnione pliki.      
   ![Obraz warunku akcji SFTP 13](./media/connectors-create-api-sftp/condition-13.png)   
9. Zapisywanie przepływu pracy tooyour zmiany hello  

