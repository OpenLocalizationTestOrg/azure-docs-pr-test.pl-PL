


## <a name="attach-an-empty-disk"></a>Dołączanie pustego dysku
Dołączanie pusty dysk jest tooadd mówiąc w uproszczeniu, danych na dysku, ponieważ Azure utworzy plik VHD hello i zapisuje go w hello konta magazynu.

1. Kliknij przycisk **maszyn wirtualnych (klasyczne)**, a następnie wybierz hello odpowiedniej maszyny Wirtualnej.

2. W menu Ustawienia powitania kliknij **dysków**.

   ![Dołącz nowy pusty dysk](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. Na pasku poleceń powitania kliknij **Dołącz nowy**.  
    Witaj **Dołączanie nowego dysku** zostanie wyświetlone okno dialogowe.

    ![Dołączanie nowego dysku](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    Wypełnij hello następujących informacji:
    - W **nazwę pliku**, zaakceptuj nazwę domyślną hello, lub wpisz inną hello pliku VHD. Hello dysku danych korzysta z użyciem nazwy wygenerowanej automatycznie, nawet wtedy, gdy wpisz inną nazwę dla pliku VHD hello.
    - Wybierz hello **typu** hello dysku danych. Wszystkie maszyny wirtualne obsługuje dyski standardowe. Wiele maszyn wirtualnych również obsługuje dysków premium.
    - Wybierz hello **rozmiar (GB)** hello dysku danych.
    - Aby uzyskać **buforowanie hosta**, wybierz Brak lub tylko do odczytu.
    - Kliknij przycisk OK toofinish.

4. Po utworzeniu i dołączyć dysku danych hello, znajduje się w sekcji dysków hello hello maszyny Wirtualnej.

   ![Pomyślnie dołączono dysk danych nowy i puste](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> Po dodaniu dysku danych, należy toolog na toohello maszyny Wirtualnej i zainicjalizować dysk hello, dzięki czemu można go używać.

## <a name="how-to-attach-an-existing-disk"></a>Porady: dołączanie istniejącego dysku
Dołączanie istniejącego dysku wymaga pliku vhd dostępnego na koncie magazynu. Użyj hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) konta magazynu toohello pliku VHD polecenia cmdlet tooupload hello. Po utworzeniu i przekazać plik VHD hello, można dołączyć tooa maszyny Wirtualnej.

1. Kliknij przycisk **maszyn wirtualnych (klasyczne)**, a następnie wybierz hello odpowiedniej maszyny wirtualnej.

2. W menu Ustawienia powitania kliknij **dysków**.

3. Na pasku poleceń powitania kliknij **Attach istniejących**.

    ![Dołączanie dysku danych](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. Kliknij przycisk **lokalizacji**. Wyświetlanie Hello dostępny magazyn kont. Następnie wybierz konto magazynu odpowiednie spośród wymienionych.

    ![Podaj konto magazynu dysku](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. A **konta magazynu** zawiera jeden lub więcej kontenerów, które zawierają dyski (VHD). Wybierz odpowiedniego kontenera hello wymienione.

    ![Podaj kontenera systemu windows wirtualnych maszyn](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. Witaj **wirtualne dyski twarde** panelu zawiera listę dysków hello przechowywany w kontenerze hello. Kliknij jeden z dysków hello, a następnie kliknij przycisk Wybierz.

    ![Przewidują obrazu dysku wirtualnego windows maszyny](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. Witaj **dołączyć istniejącego dysku** panelu ponownie, wyświetli się z lokalizacją hello zawierającego hello konta magazynu, kontenera i maszyny wirtualnej toohello tooadd wybrany dysk twardy (vhd).

  Ustaw **buforowanie hosta** toonone lub odczytu, kliknij przycisk OK.

    ![Pomyślnie dołączono dysk danych](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
