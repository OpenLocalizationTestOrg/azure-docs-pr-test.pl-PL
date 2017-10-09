Istnieją różne powody, gdy nie można uruchomić lub połączyć tooan aplikacji uruchomionych na maszynie wirtualnej platformy Azure (VM). Przyczyny obejmują aplikacji hello nie działa lub nasłuchiwania na portach hello oczekiwano hello port nasłuchujący zablokowane lub sieciowe reguły prawidłowo przekazywanie ruchu toohello aplikacji. W tym artykule opisano toofind metodyczny podejścia i poprawne hello problem.

Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej przy użyciu protokołu RDP lub SSH, zobacz jedną z następujących hello najpierw artykuły:

* [Rozwiązywanie problemów z tooa połączeń usług pulpitu zdalnego z systemem Windows Azure maszyny wirtualnej](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* [Rozwiązywanie problemów z Secure Shell (SSH) połączeń tooa opartych na systemie Linux maszyny wirtualnej platformy Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

> [!NOTE]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../articles/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu oba modele, ale firma Microsoft zaleca się, że większości nowych wdrożeń korzystać hello modelu Resource Manager.

Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello MSDN Azure i hello przepełnienie stosu fora](https://azure.microsoft.com/support/forums/). Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.

## <a name="quick-start-troubleshooting-steps"></a>Szybki start kroki rozwiązywania problemów
Jeśli masz problemy z połączeniem tooan aplikacji, spróbuj hello następujące ogólne kroki rozwiązywania problemów. Po każdym kroku spróbuj ponownie łączące aplikacji tooyour:

* Uruchom ponownie maszynę wirtualną hello
* Utwórz ponownie punkt końcowy hello / reguł zapory / sieci reguł zabezpieczeń grupy (NSG)
  * [Model usługi Resource Manager — Zarządzanie grupami zabezpieczeń sieci](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [Model klasyczny — punkty końcowe usługi zarządzania w chmurze](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* Nawiązywanie połączenia z innej lokalizacji, takiej jak innej sieci wirtualnej platformy Azure
* Wdróż ponownie maszynę wirtualną hello
  * [Wdrożenie maszyny Wirtualnej z systemem Windows](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [Wdrożenie maszyny Wirtualnej systemu Linux](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* Utwórz ponownie hello maszyny wirtualnej

Aby uzyskać więcej informacji, zobacz [Rozwiązywanie problemów z łącznością punktu końcowego (RDP/SSH/HTTP, awarii itp.)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).

## <a name="detailed-troubleshooting-overview"></a>Szczegółowe informacje dotyczące rozwiązywania problemów
Istnieją cztery główne obszary tootroubleshoot hello dostęp do aplikacji, która działa na maszynie wirtualnej platformy Azure.

![Rozwiązywanie problemów z nie można uruchomić aplikacji](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. Aplikacja Hello uruchomiona na powitania maszyny wirtualnej platformy Azure.
   * Sama aplikacja hello działa poprawnie?
2. Witaj maszyny wirtualnej platformy Azure.
   * Hello samej maszyny Wirtualnej działa poprawnie i odpowiada toorequests?
3. Punktów końcowych sieci platformy Azure.
   * Punkty końcowe usługi chmury dla maszyn wirtualnych w hello klasycznego modelu wdrożenia.
   * Grupy zabezpieczeń sieci i reguły NAT ruchu przychodzącego dla maszyn wirtualnych w modelu wdrażania usługi Resource Manager.
   * Można ruchu przepływ użytkowników toohello maszyny Wirtualnej/aplikacji hello oczekiwano portów?
4. Urządzenie brzegowe internetowej.
   * Reguły zapory w miejscu uniemożliwiają ruchu w drodze poprawnie?

Dla komputerów klienckich, które uzyskują dostęp do aplikacji hello za pośrednictwem połączenia sieci VPN i ExpressRoute lokacja lokacja hello główne obszary, które mogą być przyczyną problemów są aplikacji hello i hello maszyny wirtualnej platformy Azure.

Źródło hello toodetermine hello problemu i jego skorygowania, wykonaj następujące kroki.

## <a name="step-1-access-application-from-target-vm"></a>Krok 1: Dostęp do aplikacji z docelową maszynę Wirtualną
Spróbuj tooaccess aplikacji hello hello odpowiedniego klienta programu z hello maszyny Wirtualnej, na którym jest uruchomiony. Użyj nazwy hosta lokalnego hello, hello lokalny adres IP lub hello adres sprzężenia zwrotnego (127.0.0.1).

![Uruchom aplikację bezpośrednio z hello maszyny Wirtualnej](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

Na przykład jeśli aplikacja hello jest serwerem sieci web, otwórz przeglądarkę na powitania maszyny Wirtualnej i spróbuj tooaccess strony sieci web hostowanej na powitania maszyny Wirtualnej.

Jeśli dostęp do aplikacji hello Przejdź zbyt[krok 2](#step2).

Jeśli nie masz dostępu do aplikacji hello, sprawdź hello następujące ustawienia:

* Aplikacja Hello jest uruchomiona na powitania docelowej maszyny wirtualnej.
* Aplikacja Hello nasłuchuje na powitania oczekiwano porty TCP i UDP.

W systemach Windows i maszyn wirtualnych z systemem Linux, użyj hello **netstat -** polecenia tooshow hello aktywne porty nasłuchiwania. Sprawdź dane wyjściowe hello hello oczekiwano portów, na których powinien nasłuchiwać aplikacji. Ponowne uruchomienie aplikacji hello lub odpowiednio je skonfigurować porty hello oczekiwano toouse i spróbuj lokalnie aplikacji hello tooaccess ponownie.

## <a id="step2"></a>Krok 2: Dostęp do aplikacji z inną maszynę Wirtualną w hello tej samej sieci wirtualnej
Spróbuj tooaccess aplikacji hello z innej maszyny Wirtualnej, ale w hello sam sieci wirtualnej, przy użyciu nazwy hosta hello VM lub przypisać Azure public, private lub dostawca adres IP. Maszyny wirtualne utworzone za pomocą hello klasycznego modelu wdrażania, nie używaj dla hello publicznego adresu IP hello usługi w chmurze.

![Uruchom aplikację z innej maszyny Wirtualnej](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

Na przykład jeśli aplikacja hello jest serwerem sieci web, spróbuj tooaccess strony sieci web w przeglądarce na inną maszynę Wirtualną w hello tej samej sieci wirtualnej.

Jeśli dostęp do aplikacji hello Przejdź zbyt[kroku 3](#step3).

Jeśli nie masz dostępu do aplikacji hello, sprawdź hello następujące ustawienia:

* Zapora hosta Hello w celu hello wirtualna zezwala hello żądanie przychodzące i wychodzące odpowiedzi ruchu.
* Włamań lub oprogramowania w celu hello maszyny Wirtualnej do monitorowania sieci zezwala na ruch hello.
* Punkty końcowe usług chmury lub grupy zabezpieczeń sieci są zezwala na ruch hello:
  * [Model klasyczny — punkty końcowe usługi zarządzania w chmurze](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [Model usługi Resource Manager — Zarządzanie grupami zabezpieczeń sieci](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* Oddzielny składnik uruchomione w maszynie Wirtualnej w ścieżce hello między testem hello maszyny Wirtualnej i maszyny Wirtualnej, takie jak usługi równoważenia obciążenia lub zapora zezwala na ruch hello.

Na maszynie wirtualnej z systemem Windows użyj zapory systemu Windows z zabezpieczeniami zaawansowanymi toodetermine, czy reguły zapory hello wykluczanie aplikacji ruchu przychodzącego i wychodzącego.

## <a id="step3"></a>Krok 3: Dostęp do aplikacji z poza siecią wirtualną hello
Spróbuj aplikacji hello tooaccess z komputera spoza sieci wirtualnej hello jako hello maszyny Wirtualnej, na którym działa aplikacja hello. Przy użyciu innej sieci jako oryginalnego komputera klienckiego.

![Uruchom aplikację z komputera spoza sieci wirtualnej hello](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

Na przykład jeśli aplikacja hello jest serwerem sieci web, spróbuj tooaccess hello strony sieci web przeglądarce uruchomionej na komputerze, który nie znajduje się w sieci wirtualnej hello.

Jeśli nie masz dostępu do aplikacji hello, sprawdź hello następujące ustawienia:

* Dla maszyn wirtualnych utworzono przy użyciu hello klasycznego modelu wdrażania:
  
  * Upewnij się, że konfiguracja punktu końcowego hello powitalne wirtualna zezwala na ruch przychodzący hello, szczególnie hello protocol (TCP lub UDP) i numery portów publicznego i prywatnego hello.
  * Sprawdź, czy listy kontroli dostępu (ACL) w punkcie końcowym hello nie uniemożliwiają ruch przychodzący z hello Internet.
  * Aby uzyskać więcej informacji, zobacz [jak tooSet się punkty końcowe tooa maszyny wirtualnej](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Dla maszyn wirtualnych utworzonych przy użyciu modelu wdrażania usługi Resource Manager hello:
  
  * Sprawdź, czy który hello przychodzących konfiguracji reguły NAT dla maszyny Wirtualnej zezwala na ruch przychodzący hello, szczególnie hello protocol (TCP lub UDP) i numery portów publicznego i prywatnego hello powitalne.
  * Sprawdź hello żądanie przychodzące i wychodzące odpowiedzi ruchu umożliwia grup zabezpieczeń sieci.
  * Aby uzyskać więcej informacji, zobacz [What is a Network Security Group (NSG)?](../articles/virtual-network/virtual-networks-nsg.md) (Co to jest sieciowa grupa zabezpieczeń?).

Jeśli hello maszyny wirtualnej lub punktu końcowego jest członkiem zestawu z równoważeniem obciążenia:

* Sprawdź, czy hello sondowania protocol (TCP lub UDP) i numer portu są poprawne.
* Jeśli sondowania hello protokół i port różni się od hello zestawu o zrównoważonym obciążeniu protokół i port:
  * Sprawdź, czy aplikacja hello nasłuchuje na powitania sondowania protocol (TCP lub UDP) i numer portu (Użyj **polecenie netstat – a** na powitania docelowa maszyna wirtualna).
  * Sprawdź, czy Zapora hosta hello w celu hello, które maszyna wirtualna zezwala na żądania przychodzące sondowania hello i badania ruchu wychodzącego ruchu odpowiedzi.

Jeśli uzyskujesz dostęp do aplikacji hello, upewnij się, czy zezwala na urządzenie brzegowe internetowej:

* ruch żądania wychodzącego aplikacji Hello z Twojej toohello komputera klienta maszyny wirtualnej platformy Azure.
* Witaj ruch odpowiedzi aplikacji dla ruchu przychodzącego z hello maszyny wirtualnej platformy Azure.

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a>Krok 4. Jeśli nie masz dostępu do aplikacji hello, użyj Sprawdź IP toocheck hello ustawień. 

Aby uzyskać więcej informacji, zobacz [omówienie monitorowania sieci platformy Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="additional-resources"></a>Dodatkowe zasoby
[Rozwiązywanie problemów z tooa połączeń usług pulpitu zdalnego z systemem Windows Azure maszyny wirtualnej](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[Rozwiązywanie problemów z Secure Shell (SSH) połączeń tooa opartych na systemie Linux maszyny wirtualnej platformy Azure](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

