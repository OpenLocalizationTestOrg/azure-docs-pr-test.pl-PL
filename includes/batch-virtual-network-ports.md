- Sieć wirtualna musi znajdować się w tym samym **regionie** i tej samej **subskrypcji** platformy Azure, co konto usługi Batch.

- W przypadku pul utworzonych za pomocą konfiguracji maszyny wirtualnej obsługiwane są tylko sieci wirtualne oparte na usłudze Azure Resource Manager. W przypadku pul utworzonych za pomocą konfiguracji usługi w chmurze są obsługiwane tylko klasyczne sieci wirtualne. 
  
- Aby można było użyć klasycznej sieci wirtualnej, jednostka usługi `MicrosoftAzureBatch` musi mieć rolę `Classic Virtual Machine Contributor` z kontrolą dostępu opartą na rolach (RBAC) dla określonej sieci wirtualnej. Jednak do używania sieci wirtualnej opartej na usłudze Azure Resource Manager nie jest wymagana dodatkowa konfiguracja uprawnień.

- Podsieć określona dla puli musi mieć wystarczającą liczbę nieprzypisanych adresów IP do obsługi maszyn wirtualnych przeznaczony dla puli, czyli sumę właściwości puli `targetDedicatedNodes` i `targetLowPriorityNodes`. Jeśli podsieć nie ma wystarczającej liczby nieprzypisanych adresów IP, pula częściowo przydzieli węzły obliczeniowe, a następnie wystąpi błąd dotyczący zmiany rozmiaru. 

- Sieć wirtualna musi zezwalać na komunikację z usługą Batch, aby umożliwiać planowanie zadań w węzłach obliczeniowych. Można to sprawdzić przez upewnienie się, że sieć wirtualna ma skojarzone sieciowe grupy zabezpieczeń. Jeśli komunikacja z węzłami obliczeniowymi w określonej podsieci zostanie odrzucona przez sieciową grupę zabezpieczeń, usługa Batch ustawi stan węzłów obliczeniowych na **nienadające się do użytku**. 

- Jeśli określona sieć wirtualna ma skojarzone sieciowe grupy zabezpieczeń i/lub zaporę, skonfiguruj porty przychodzące i wychodzące tak, jak pokazano w poniższych tabelach:


  |    Porty docelowe    |    Źródłowy adres IP      |   Port źródłowy    |    Czy usługa Batch dodaje sieciowe grupy zabezpieczeń?    |    Wymagane do korzystania z maszyny wirtualnej?    |    Akcja użytkownika   |
  |---------------------------|---------------------------|----------------------------|----------------------------|-------------------------------------|-----------------------|
  |   <ul><li>W przypadku pul utworzonych za pomocą konfiguracji maszyny wirtualnej: 29876, 29877</li><li>W przypadku pul utworzonych za pomocą konfiguracji usług w chmurze: 10100, 20100, 30100</li></ul>        |    Tylko adresy IP roli usługi Batch | * lub 443 |    Tak. Usługa Batch dodaje sieciowe grupy zabezpieczeń na poziomie interfejsów sieciowych (kart sieciowych) dołączonych do maszyn wirtualnych. Te sieciowe grupy zabezpieczeń zezwalają tylko na ruch z adresów IP roli usługi Batch. Nawet jeśli otworzysz te porty dla całego Internetu, ruch zostanie zablokowany na poziomie karty sieciowej. |    Tak  |  Nie musisz określać sieciowej grupy zabezpieczeń, ponieważ usługa Batch zezwala tylko na adresy IP usługi Batch. <br /><br /> Jeśli jednak określisz sieciową grupę zabezpieczeń, upewnij się, że te porty zostały otwarte na potrzeby ruchu przychodzącego. <br /><br /> Jeśli wybierzesz * jako źródłowy adres IP w sieciowej grupie zabezpieczeń, usługa Batch również doda sieciowe grupy zabezpieczeń na poziomie kart sieciowych dołączonych do maszyn wirtualnych. |
  |    3389 (Windows), 22 (Linux)               |    Maszyny użytkownika używane dla celów debugowania, dzięki czemu można uzyskiwać zdalny dostęp do maszyny wirtualnej.    |   *  | Nie                                    |    Nie                    |    Dodaj sieciowe grupy zabezpieczeń, jeśli chcesz zezwolić na zdalny dostęp (RDP lub SSH) do maszyny wirtualnej.   |                                


  |    Porty ruchu wychodzącego    |    Element docelowy    |    Czy usługa Batch dodaje sieciowe grupy zabezpieczeń?    |    Wymagane do korzystania z maszyny wirtualnej?    |    Akcja użytkownika    |
  |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
  |    443    |    Azure Storage    |    Nie    |    Tak    |    Jeśli dodasz sieciowe grupy zabezpieczeń, sprawdź, czy ten port został otwarty na potrzeby ruchu wychodzącego.    |

   Upewnij się również, że punkt końcowy usługi Azure Storage może zostać rozpoznany przez dowolne niestandardowe serwery DNS, które obsługują sieć wirtualną. W szczególności rozpoznawalne powinny być adresy URL formularzy `<account>.table.core.windows.net`, `<account>.queue.core.windows.net` i `<account>.blob.core.windows.net`. 

   Jeśli dodasz Menedżera zasobów na podstawie grupy NSG, istnieje możliwość stosowania [usługi tagi](../articles/virtual-network/security-overview.md#service-tags) wybierz adresy IP magazynu dla konkretnego regionu połączeń wychodzących. Należy pamiętać, że adresy IP magazynu musi być tym samym regionie co Twoje konto usługi partia zadań i sieci wirtualnej. Tagi usługi są obecnie w wersji zapoznawczej w wybranych regionach platformy Azure.