Na platformie Azure jest teraz dostępna obsługa dwóch funkcji debugowania: obsługa danych wyjściowych konsoli i zrzutu ekranu dla modelu wdrażania przy użyciu usługi Azure Virtual Machines Resource Manager. 

Podczas przełączania tooAzure własny obraz lub nawet rozruch jeden z obrazów platformy hello, może istnieć wiele przyczyn, dlaczego pobiera maszynę wirtualną do stanu rozruchowego. Te funkcje włączenia należy tooeasily diagnozowanie i odzyskiwanie po błędach rozruchu maszyn wirtualnych.

Dla maszyn wirtualnych systemu Linux można łatwo przeglądać dane wyjściowe hello dziennika konsoli z hello portalu:

![Azure Portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
Jednak dla systemów Windows i maszyn wirtualnych systemu Linux Azure umożliwia również toosee hello maszyny Wirtualnej z funkcji hypervisor hello zrzut ekranu:

![Błąd](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

Obie te funkcje są obsługiwane dla maszyn wirtualnych platformy Azure we wszystkich regionach. Uwaga, zrzuty ekranu i danych wyjściowych może potrwać too10 tooappear minut na koncie magazynu.

## <a name="common-boot-errors"></a>Typowe błędy rozruchu

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [Nie znaleziono systemu operacyjnego](https://support.microsoft.com/help/4010142)
- [Niepowodzenie rozruchu lub błąd INACCESSIBLE_BOOT_DEVICE](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Włączanie diagnostyki na nowej maszynie wirtualnej
1. Podczas tworzenia nowej maszyny wirtualnej z hello portalu w wersji zapoznawczej, wybierz hello **usługi Azure Resource Manager** z listy rozwijanej modelu wdrażania hello:
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. Skonfiguruj te pliki diagnostyczne hello miejsce chcesz tooplace monitorowanie opcja tooselect hello magazynu konta.
 
    ![Tworzenie maszyny wirtualnej](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. Jeśli wdrażasz za pomocą szablonu usługi Azure Resource Manager, przejdź tooyour zasobu maszyny wirtualnej i Dołącz sekcji profilu diagnostyki hello. Należy pamiętać, nagłówek wersji interfejsu API toouse hello "2015-06-15".

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. profilu diagnostyki Hello umożliwia konta magazynu hello tooselect miejscu tooput tych dzienników.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

toodeploy próbkę maszyny wirtualnej z włączoną, diagnostykę rozruchu wyewidencjonowanie naszym repozytorium, w tym miejscu.

## <a name="update-an-existing-virtual-machine"></a>Aktualizowanie istniejącej maszyny wirtualnej ##

tooenable diagnostyki rozruchu za pomocą hello portalu, można także zaktualizować istniejącej maszyny wirtualnej za pośrednictwem hello portalu. Wybierz hello diagnostyki rozruchu opcji i Zapisz. Uruchom ponownie hello wirtualna tootake efekt.

![Aktualizowanie istniejącej maszyny wirtualnej](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

