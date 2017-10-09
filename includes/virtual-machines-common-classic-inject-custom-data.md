


W tym temacie opisano sposób:

* Wstaw danych do maszyny wirtualnej platformy Azure (VM), gdy jest inicjowana.
* Pobrać do systemów Windows i Linux.
* Użyj specjalnego narzędzi dostępnych w niektórych systemach toodetect i automatycznie obsługiwać danych niestandardowych.

> [!NOTE]
> W tym artykule opisano sposób niestandardowe dane mogą zostać dodane przy użyciu maszyny Wirtualnej utworzonej z hello interfejs API zarządzania usługami Azure. toosee toouse hello Azure API Management zasobów, zobacz temat [hello przykładowy szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Wstrzykiwania niestandardowe dane do maszyny wirtualnej platformy Azure
Ta funkcja jest obecnie obsługiwane tylko w hello [interfejsu wiersza polecenia platformy Azure](https://github.com/Azure/azure-xplat-cli). W tym miejscu utworzymy `custom-data.txt` pliku, który zawiera danych, następnie wstrzyknąć który w toohello maszyny Wirtualnej podczas inicjowania obsługi. Mimo że można użyć opcji hello na powitania `azure vm create` polecenia hello poniżej pokazano, jednym z podejść bardzo podstawowe:

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>W maszynie wirtualnej hello przy użyciu niestandardowych danych
* Jeśli maszyna wirtualna Azure jest Maszynę wirtualną z systemem Windows, a następnie hello niestandardowych danych zostanie zapisany za`%SYSTEMDRIVE%\AzureData\CustomData.bin`. Mimo że był algorytmem Base64 tootransfer z toohello komputera lokalnego hello nowej maszyny Wirtualnej, jest automatycznie zdekodować i można otworzyć lub użyć natychmiast.
  
  > [!NOTE]
  > Jeśli plik hello istnieje, zostanie zastąpiony. zabezpieczenia Hello katalogu hello są skonfigurowane za**systemu: Pełna kontrola** i **Administratorzy: Pełna kontrola**.
  > 
  > 
* W przypadku maszyny Wirtualnej Azure opartych na systemie Linux maszyny Wirtualnej, a następnie plik danych niestandardowych hello będą znajdować się w jednej z następujących hello umieszcza w zależności od Twojego distro. Witaj dane mogą być algorytmem Base64, może więc być konieczny danych hello toodecode najpierw:
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Inicjowania chmurze na platformie Azure
W przypadku maszyny Wirtualnej Azure z obrazu Ubuntu lub CoreOS, można użyć toosend CustomData inicjowaniem toocloud konfiguracji chmury. Lub jeśli plik danych niestandardowych jest skryptem, następnie init chmury można po prostu wykonywania.

### <a name="ubuntu-cloud-images"></a>Obrazy Ubuntu chmury
W większości obrazów systemu Linux platformy Azure, możesz edytować "/ etc/waagent.conf" tooconfigure hello zasobów dysku i zamiany pliku. Zobacz [Podręcznik użytkownika agenta systemu Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Aby uzyskać więcej informacji.

Jednak na powitania Ubuntu chmury obrazów, należy użyć init chmury tooconfigure hello zasobu dysku (to znaczy hello "tymczasowych" dysk) i wymiany partycji. Zobacz następujące strony w witrynie wiki Ubuntu hello szczegółowe hello: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>Następne kroki: przy użyciu inicjowania chmury
Aby uzyskać więcej informacji, zobacz hello [init chmury dokumentacji Ubuntu](https://help.ubuntu.com/community/CloudInit).

<!--Link references-->
[Dodaj dokumentacja interfejsu API REST zarządzania usługi roli](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Interfejs wiersza polecenia platformy Azure](https://github.com/Azure/azure-xplat-cli)

