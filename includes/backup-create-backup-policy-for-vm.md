## <a name="defining-a-backup-policy"></a>Określanie zasad tworzenia kopii zapasowych
Zasady tworzenia kopii zapasowych określają macierz z informacjami po są pobierane migawki danych hello i jak długo są przechowywane. W przypadku określania zasad tworzenia kopii zapasowych maszyny wirtualnej można wyzwolić zadanie tworzenia kopii zapasowej *raz dziennie*. Podczas tworzenia nowych zasad jest stosowane toohello magazynu. Interfejs zasad tworzenia kopii zapasowej Hello wygląda następująco:

![Zasady tworzenia kopii zapasowych](./media/backup-create-policy-for-vms/backup-policy.png)

toocreate zasady:

1. Wprowadź nazwę hello **Nazwa zasady**.
2. Migawki danych mogą być pobierane raz dziennie lub co tydzień. Użyj hello **częstotliwość wykonywania kopii zapasowych** toochoose menu rozwijane czy migawki mają być pobierane raz dziennie lub co tydzień.
   
   * Jeśli wybierzesz pobieranie raz dziennie, użyj hello podświetlony formant tooselect hello porę dnia, hello hello migawki. toochange hello godzinę, usuń zaznaczenie pola wyboru hello godzinę i wybierz nową hello.
     
     ![Zasady tworzenia kopii zapasowych raz dziennie](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * Jeśli wybierzesz tydzień, użyj hello wyróżnionych kontrolek tooselect hello dni tygodnia hello i hello godzinę dnia tootake hello migawki. W menu dzień hello wybierz jeden lub kilka dni. W menu godzina hello wybierz jedną godzinę. toochange hello godzinę, usuń zaznaczenie pola wyboru hello wybranego godzinę i wybierz nową hello.
     
     ![Zasady tworzenia kopii zapasowych co tydzień](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. Domyślnie wszystkie opcje **Zakres przechowywania** są zaznaczone. Usuń zaznaczenie pola wyboru limitu zakresu przechowywania, nie ma toouse. Następnie określ hello toouse odstępy czasu.
   
    Miesięczne i roczne zakresy przechowywania umożliwiają migawki hello toospecify oparte na przyrostu tygodniowego lub dziennego.
   
   > [!NOTE]
   > W przypadku ochrony maszyn wirtualnych zadanie tworzenia kopii zapasowej jest uruchamiane raz dziennie. czas powitania po hello kopii zapasowej jest hello takie same dla każdego zakresu przechowywania.
   > 
   > 
4. Po ustawieniu wszystkich opcji zasad hello u góry bloku hello powitania kliknij **zapisać**.
   
    nowe zasady Hello jest natychmiast zastosowane toohello magazynu.

