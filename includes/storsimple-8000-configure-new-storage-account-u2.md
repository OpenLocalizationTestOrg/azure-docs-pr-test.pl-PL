<!--author=alkohli last changed: 01/20/17-->


#### <a name="to-add-a-storage-account-credential-in-the-same-azure-subscription-as-the-storsimple-device-manager-service"></a>Aby dodać poświadczenia konta magazynu w tej samej subskrypcji platformy Azure jako usługa Menedżer urządzeń StorSimple

1. Przejdź do usługi Menedżer urządzeń StorSimple. W sekcji **Konfiguracja** kliknij pozycję **Poświadczenia konta magazynu**.

    ![Poświadczenia konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct1.png)

2. W bloku **Poświadczenia konta magazynu** kliknij pozycję **+ Dodaj**.

    ![Dodawanie poświadczeń konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct2.png)

3. W bloku **Dodawanie poświadczenia konta magazynu** wykonaj następujące kroki:

    1. Ponieważ dodajesz poświadczenie konta magazynu w tej samej subskrypcji platformy Azure co usługa, upewnij się, że pole **Bieżące** zostało zaznaczone.

    2. Z listy rozwijanej **kont magazynu** wybierz istniejące konto magazynu.

    3. W oparciu o wybrane konto magazynu zostanie wyświetlona **lokalizacja** (wyszarzona— nie można jej zmienić w tym miejscu).

    4. Wybierz opcję **Włącz tryb SSL**, aby utworzyć bezpieczny kanał komunikacji sieciowej między urządzeniem i chmurą. Wyłącz opcję **Włącz protokół SSL** tylko, jeśli pracujesz w chmurze prywatnej.

        ![Blok dodawania poświadczeń konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct3.png)

    5. Kliknij pozycję **Dodaj**, aby uruchomić zadanie tworzenia dla poświadczenia konta magazynu. Po pomyślnym utworzeniu poświadczenia konta magazynu otrzymasz powiadomienie.

        ![Powiadomienie o powodzeniu dla poświadczeń konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct5.png)

Nowo utworzone konto magazynu zostanie wyświetlone w obszarze listy **Poświadczenia konta magazynu**.

![Lista poświadczeń konta magazynu](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct6.png)

