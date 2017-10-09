



W zależności od środowiska i dostępnych wyborów hello skryptu można utworzyć wszystkich infrastruktury klastra hello, w tym hello sieci wirtualnej platformy Azure, konta magazynu usługi w chmurze, kontrolera domeny, lokalnych lub zdalnych baz danych SQL, węzła głównego i dodatkowego klastra węzły. Alternatywnie hello skryptu można użyć istniejącej infrastruktury platformy Azure i utworzyć tylko hello węzłów klastra HPC.

Informacje uzupełniające dotyczące Planowanie klastra HPC Pack, zobacz hello [wersja ewaluacyjna produktu i planowanie](https://technet.microsoft.com/library/jj899596.aspx) i [wprowadzenie](https://technet.microsoft.com/library/jj899590.aspx) zawartości w bibliotece TechNet HPC Pack 2012 R2 hello.

## <a name="prerequisites"></a>Wymagania wstępne
* **Subskrypcja platformy Azure**: subskrypcji można używać w obu hello usługi Azure globalnym, ani w chińskiej wersji platformy Azure. Swoje limity subskrypcji wpływa na powitania liczbę i rodzaj węzłach klastra, którą można wdrożyć. Aby uzyskać informacje, zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../articles/azure-subscription-service-limits.md).
* **Komputer kliencki z systemem Windows przy użyciu programu Azure PowerShell 0.8.10 lub nowszy zainstalowany i skonfigurowany**: zobacz [wprowadzenie do programu Azure PowerShell](/powershell/azureps-cmdlets-docs) dla instalacji instrukcje i kroki tooconnect tooyour subskrypcji platformy Azure.
* **Skrypt wdrożenia HPC Pack IaaS**: Pobierz i Rozpakuj hello najnowszą wersję hello skryptu z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Sprawdź wersję hello skryptu hello uruchamiając `New-HPCIaaSCluster.ps1 –Version`. Ten artykuł jest oparty na wersji 4.5.2 hello skryptu.
* **Konfiguracja pliku**: Utwórz plik XML, że skrypt hello używa klastra HPC hello tooconfigure. Informacje i przykłady zobacz sekcje w dalszej części tego artykułu i hello plik Manual.rtf dołączony hello skrypt wdrożenia.

## <a name="syntax"></a>Składnia
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> Uruchom skrypt hello jako administrator.
> 
> 

### <a name="parameters"></a>Parametry
* **ConfigFile**: Określa ścieżkę pliku hello klastra HPC hello toodescribe hello konfiguracji pliku. Zobacz więcej informacji na temat hello pliku konfiguracji, w tym temacie lub w pliku hello Manual.rtf w folderze hello zawierający skrypt hello.
* **AdminUserName**: Określa nazwę użytkownika, powitalne. Jeśli hello domeny lasu został utworzony przez skrypt hello, staje się on hello nazwą użytkownika administratora lokalnego dla wszystkich maszyn wirtualnych i nazwę administratora domeny hello. Jeśli hello lasu domeny już istnieje, to określa użytkownika domeny hello hello tooinstall nazwa użytkownika administratora lokalnego HPC Pack.
* **AdminPassword**: Określa hasło administratora hello. Jeśli nie zostanie określony w wierszu polecenia hello, skrypt hello monituje tooinput hello hasła.
* **HPCImageName** (opcjonalnie): Określa nazwę obrazu maszyny Wirtualnej pakietu HPC hello używany klaster HPC hello toodeploy. Musi być obrazem udostępnionych przez firmę Microsoft HPC Pack z hello Azure Marketplace. Jeśli nie została określona (zalecane zwykle), hello skryptu wybiera hello Najnowsza opublikowana [obrazu HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/). Obraz najnowsze Hello jest oparty na Windows Server 2012 R2 Datacenter z HPC Pack 2012 R2 Update 3.
  
  > [!NOTE]
  > Wdrożenie zakończy się niepowodzeniem, jeśli nie określisz prawidłowym obrazem HPC Pack.
  > 
  > 
* **Plik dziennika** (opcjonalnie): Określa ścieżkę pliku dziennika wdrażania hello. Jeśli nie zostanie określony, hello skrypt tworzy plik dziennika w katalogu temp hello hello komputera z uruchomionym hello skryptu.
* **Wymuś** (opcjonalnie): pomija wszystkie monity potwierdzenie hello.
* **NoCleanOnFailure** (opcjonalnie): Określa, w tym hello maszynach wirtualnych platformy Azure, które nie zostały pomyślnie wdrożone nie zostaną usunięte. Ręcznie usuń te maszyny wirtualne przed uruchomienie hello skryptu toocontinue hello wdrożenia lub hello wdrożenia może zakończyć się niepowodzeniem.
* **PSSessionSkipCACheck** (opcjonalnie): dla każdej usługi w chmurze z maszyn wirtualnych wdrożonych przez ten skrypt certyfikatu z podpisem własnym jest generowany automatycznie przez usługę Azure i hello wszystkich maszyn wirtualnych w usłudze w chmurze hello użycie tego certyfikatu jako hello domyślne systemu Windows Zdalne zarządzanie systemem Windows (WinRM) certyfikatu. Funkcje HPC toodeploy na tych maszynach wirtualnych Azure, skrypt hello domyślnie tymczasowo zainstaluje te certyfikaty w hello komputera lokalnego\\magazynie Zaufane główne urzędy certyfikacji powitania klienta komputera toosuppress Witaj "nie jest zaufany urząd certyfikacji" zabezpieczeń Błąd podczas wykonywania skryptu. Hello certyfikaty zostaną usunięte po zakończeniu hello skryptu. Jeśli ten parametr jest określony, hello certyfikaty nie są zainstalowane w komputerze klienckim hello i ostrzeżenie o zabezpieczeniach hello jest pomijane.
  
  > [!IMPORTANT]
  > Ten parametr nie jest zalecane w przypadku wdrożeń produkcyjnych.
  > 
  > 

### <a name="example"></a>Przykład
Witaj poniższy przykład tworzy klastra HPC Pack przy użyciu pliku konfiguracji *MyConfigFile.xml*i określa poświadczenia administratora dla instalowanie hello klastra.

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>Dodatkowe zagadnienia
* skrypt Hello Opcjonalnie można udostępnić przesyłanie zadań za pomocą portalu internetowego HPC Pack hello lub hello HPC Pack REST API.
* Witaj opcjonalnie skryptu niestandardowych skryptów przed i po konfiguracji w węźle głównym hello tooinstall dodatkowego oprogramowania lub skonfigurować inne ustawienia.

## <a name="configuration-file"></a>Plik konfiguracji
plik konfiguracji Hello skrypt wdrożenia hello jest plik XML. plik schematu Hello HPCIaaSClusterConfig.xsd znajduje się w folderze skryptów wdrażania HPC Pack IaaS hello. **IaaSClusterConfig** jest elementem głównym hello hello pliku konfiguracji, który zawiera elementy podrzędne hello opisano szczegółowo w pliku hello Manual.rtf w folderze skryptów wdrażania hello.

