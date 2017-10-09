---
title: "aaaTroubleshoot grup zabezpieczeń sieci - Portal | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak grup zabezpieczeń sieci tootroubleshoot we wdrożeniu usługi Azure Resource Manager hello modelu przy użyciu hello portalu Azure."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: a54feccf-0123-4e49-a743-eb8d0bdd1ebc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 0d3d2110fe1507f36e3b933de924a0876db2747a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-hello-azure-portal"></a>Rozwiązywanie problemów z grup zabezpieczeń sieci przy użyciu hello portalu Azure
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Jeśli skonfigurowana grup zabezpieczeń sieci (NSG) na maszynie wirtualnej (VM) i występują problemy z połączeniem maszyny Wirtualnej, ten artykuł zawiera omówienie funkcji diagnostyki dla grup NSG toohelp dalsze poszukiwanie rozwiązania problemu.

Grupy NSG pozwalają toocontrol hello rodzaje ruchu przepływające i maszyn wirtualnych (VM). Grupy NSG mogą być zastosowane toosubnets w sieci wirtualnej platformy Azure (VNet) i/lub interfejsów sieciowych (NIC). Hello tooa skuteczne reguły stosowane karty Sieciowej są hello reguł, które istnieją w hello zastosować grupy NSG tooa kart Sieciowych i hello podsieci, w której jest dołączona do agregacji. Reguły w tych grup NSG można czasami konflikt ze sobą i mieć wpływ na łączność sieciową z maszyny Wirtualnej.  

Można wyświetlić wszystkie reguły efektywnym elementem systemu zabezpieczeń hello z grup NSG, jak stosować kart sieciowych maszyny Wirtualnej. W tym artykule opisano, jak przy użyciu tych reguł w problemy z łącznością wirtualna tootroubleshoot hello modelu wdrażania usługi Azure Resource Manager. Jeśli nie znasz z sieci wirtualnej i NSG pojęcia, przeczytaj hello [sieci wirtualnej](virtual-networks-overview.md) i [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) omówienie artykułów.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Przy użyciu przepływu ruchu maszyny Wirtualnej tootroubleshoot skuteczne reguły zabezpieczeń
Hello scenariusz, w którym następuje jest przykładem to powszechny problem połączenia:

Maszyna wirtualna o nazwie *VM1* jest częścią podsieci o nazwie *podsieć1* w ramach sieci wirtualnej o nazwie *WestUS VNet1*. Próba tooconnect toohello maszyny Wirtualnej przy użyciu protokołu RDP za pośrednictwem portu 3389 protokołu TCP nie powiedzie się. Grupy NSG są stosowane w obu hello kart *VM1 NIC1* i hello podsieci *podsieć1*. Ruch tooTCP portu 3389 jest dozwolony w hello grupy NSG skojarzonej z interfejsem sieciowym hello *VM1 NIC1*, jednak TCP polecenie ping na tooVM1 portu 3389 kończy się niepowodzeniem.

Gdy w tym przykładzie korzysta z portu 3389 protokołu TCP, hello następujących kroków można używane toodetermine błędów połączenia przychodzącego i wychodzącego przez dowolnego portu.

### <a name="vm"></a>Wyświetl reguły efektywnym elementem systemu zabezpieczeń dla maszyny wirtualnej
Wykonaj hello następujące kroki tootroubleshoot grup NSG dla maszyny Wirtualnej:

Pełna lista reguł efektywnym elementem systemu zabezpieczeń hello można wyświetlić karty sieciowej, z hello samej maszyny Wirtualnej. Można również dodawanie, modyfikowanie i usuwanie reguły NSG podsieci i karty w bloku skuteczne reguły hello, jeśli masz uprawnienia tooperform te operacje.

1. Toohello logowania portalu Azure w https://portal.azure.com.
2. Kliknij przycisk **więcej usług**, następnie kliknij przycisk **maszyn wirtualnych** na liście hello.
3. Wybierz z listy hello tootroubleshoot maszyny Wirtualnej i zostanie wyświetlony blok maszyny Wirtualnej, z opcjami.
4. Kliknij przycisk **Diagnozuj & rozwiązywania problemów** , a następnie wybierz powszechny problem. Na przykład **toomy maszyny Wirtualnej systemu Windows nie można połączyć z** jest zaznaczone. 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image1.png)
5. Kroki są wyświetlane w polu hello problem, jak pokazano na poniższej ilustracji hello: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image2.png)
   
    Kliknij przycisk *efektywnym elementem systemu zabezpieczeń, zasady grupy* hello liście zalecanych kroków.
6. Witaj **pobieranie reguł efektywnym elementem systemu zabezpieczeń** zostanie wyświetlony blok, jak pokazano na poniższej ilustracji hello:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image3.png)
   
    Następujące sekcje obraz powitania hello powiadomień:
   
   * **Zakres:** ustawić także*VM1*, hello maszyny Wirtualnej wybrany w kroku 3.
   * **Interfejs sieciowy:** *VM1 NIC1* jest zaznaczone. Maszyna wirtualna może mieć wiele interfejsów sieciowych (NIC). Poszczególne karty Sieciowe mogą mieć unikatowe efektywnym elementem systemu zabezpieczeń reguły. Podczas rozwiązywania problemów, konieczne może tooview hello efektywnym elementem systemu zabezpieczeń reguł dla poszczególnych kart sieciowych.
   * **Grupy NSG skojarzone:** grupy NSG mogą być zastosowane tooboth hello kart Sieciowych i hello podsieci hello jest połączona karta sieciowa. Na rysunku hello grupy NSG została tooboth zastosowane hello kart Sieciowych i hello podsieci, w której jest dołączona do. Możesz kliknąć na nazwy grupy NSG hello toodirectly zmodyfikuj zasady w hello grup NSG.
   * **Karta VM1 nsg:** hello listę reguł wyświetlonych obraz powitania jest hello grupa NSG stosowana toohello karty sieciowej. Kilka reguł domyślnych są tworzone przez usługę Azure zawsze, gdy grupa NSG jest tworzona. Nie można usunąć reguły domyślne hello, ale można je zastąpić przy użyciu reguł o wyższym priorytecie. więcej informacji na temat reguł domyślnych, przeczytaj hello toolearn [omówienie NSG](virtual-networks-nsg.md#default-rules) artykułu.
   * **Kolumna docelowa:** niektóre reguły hello mają tekst w kolumnie hello, podczas gdy inne muszą prefiksy adresów. tekst Hello jest hello nazwę domyślną regułę zabezpieczeń toohello znaczniki zastosowane podczas jej tworzenia. tagi Hello są dostarczane przez system identyfikatorów, które reprezentują wiele prefiksów. Wybranie reguły za pomocą tagów, takich jak *AllowInternetOutBound*, zawiera listę prefiksów hello hello **prefiksy adresów** bloku.
   * **Pobieranie:** hello lista reguł może trwać długo. Plik CSV reguł hello celów analizy offline można pobrać po kliknięciu **Pobierz** i zapisanie pliku hello.
   * **AllowRDP** reguły dla ruchu przychodzącego: ta zasada umożliwia toohello połączeń protokołu RDP maszyny Wirtualnej.
7. Kliknij przycisk hello **NSG podsieć1** kartę tooview hello skuteczne reguły z hello NSG stosowane toohello podsieci, pokazane na poniższej ilustracji hello: 
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image4.png)
   
    Powiadomienie hello *denyRDP* **przychodzący** reguły. Reguły ruchu przychodzącego na powitania podsieci są obliczane przed zasady stosowane na powitania interfejsu sieciowego. Ponieważ w podsieci hello jest stosowana reguła odmowy hello, hello żądania tooconnect tooTCP 3389 nie powiedzie się, ponieważ hello regułę Zezwalaj na powitalne nigdy nie jest obliczane karty Sieciowej. 
   
    Witaj *denyRDP* reguła jest przyczyna hello Dlaczego hello połączenie RDP kończy się niepowodzeniem. Usunięcie go powinno rozwiązać hello problem.
   
   > [!NOTE]
   > Jeśli hello maszyny Wirtualnej skojarzone z hello NIC nie jest w stanie uruchomienia, lub grupy NSG nie zostały zastosowane toohello karty Sieciowej lub podsieci, są wyświetlane żadne reguły.
   > 
   > 
8. reguły NSG tooedit, kliknij przycisk *NSG podsieć1* w hello **skojarzonych grup NSG** sekcji.
   Spowoduje to otwarcie hello **NSG podsieć1** bloku. Reguły hello można bezpośrednio edytować, klikając **reguły zabezpieczeń dla ruchu przychodzącego**.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image7.png)
9. Po usunięciu hello *denyRDP* reguły dla ruchu przychodzącego w hello **NSG podsieć1** i dodawanie *allowRDP* reguły listy reguł efektywne hello wygląda hello poniższej ilustracji:
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image8.png)
   
    Upewnij się, że portu 3389 protokołu TCP jest otwarty przez otwarcie toohello połączenia RDP maszyny Wirtualnej lub za pomocą narzędzia narzędzia PsPing hello. Użytkownik może dowiedzieć się więcej o narzędzia PsPing za odczytywanie hello [stronę pobierania narzędzia PsPing](https://technet.microsoft.com/sysinternals/psping.aspx).

### <a name="nic"></a>Wyświetl reguły efektywnym elementem systemu zabezpieczeń dla interfejsu sieciowego
Jeśli do ruchu maszyny Wirtualnej jest w pełni funkcjonalne dla określonych kart interfejsu Sieciowego, można wyświetlić pełną listę hello Zasady efektywne hello karty Sieciowej z kontekstu interfejsów sieciowych hello, wykonując następujące kroki hello:

1. Toohello logowania portalu Azure w https://portal.azure.com.
2. Kliknij przycisk **więcej usług**, następnie kliknij przycisk **interfejsy sieciowe** na liście hello.
3. Wybierz interfejs sieciowy. W poniższej ilustracji hello, karta sieciowa o nazwie *VM1 NIC1* jest zaznaczone.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image5.png)
   
    Zwróć uwagę, że hello **zakres** ustawiono wybrany interfejs sieciowy toohello. więcej informacji o toolearn hello dodatkowe informacje wyświetlane, przeczytaj kroku 6 hello **Rozwiązywanie problemów z grup NSG dla maszyny Wirtualnej** sekcji tego artykułu.
   
   > [!NOTE]
   > Usunięcie grupy NSG z interfejsem sieciowym podsieci hello grupa NSG jest nadal wprowadza ją na powitania podanych kart sieciowych. W takim przypadku dane wyjściowe hello czy wyświetla tylko reguły z podsieci hello NSG. Reguły są wyświetlane tylko, jeśli hello karty Sieciowej jest dołączony tooa maszyny Wirtualnej.
   > 
   > 
4. Zasady można edytować bezpośrednio do grupy zabezpieczeń sieci skojarzonych z karty Sieciowej i podsieci. jak to zrobić, przeczytaj toolearn krok 8 hello **wyświetlić reguły efektywnym elementem systemu zabezpieczeń dla maszyny wirtualnej** sekcji tego artykułu.

## <a name="nsg"></a>Wyświetlanie efektywnym elementem systemu zabezpieczeń reguł sieciowej grupy zabezpieczeń (NSG)
Podczas modyfikowania reguły NSG, może być tooreview hello wpływ zasad hello dodawany na określonej maszynie Wirtualnej. Można wyświetlić pełną listę hello efektywnym elementem systemu zabezpieczeń reguły dla wszystkich hello karty sieciowe obsługujące danego grupa NSG jest stosowana do, bez konieczności kontekst tooswitch od hello podane NSG bloku. tootroubleshoot skuteczne reguły w obrębie grupy NSG, pełną hello następujące kroki:

1. Toohello logowania portalu Azure w https://portal.azure.com.
2. Kliknij przycisk **więcej usług**, następnie kliknij przycisk **sieciowej grupy zabezpieczeń** na liście hello.
3. Wybierz grupy NSG. W poniższej ilustracji hello grupy NSG o nazwie grupy nsg VM1 został wybrany.
   
    ![](./media/virtual-network-nsg-troubleshoot-portal/image6.png)
   
    Następujące sekcje hello poprzedni obraz powitania powiadomień:
   
   * **Zakres:** ustawić toohello wybrane grupy NSG.
   * **Maszyna wirtualna:** gdy grupa NSG jest stosowane tooa podsieci, jest tooall stosowane interfejsy tooall dołączone maszyn wirtualnych połączonych toohello podsieci. Ta lista zawiera ta grupa NSG jest stosowana do wszystkich maszyn wirtualnych. Możesz wybrać żadnej maszyny Wirtualnej z listy hello.
     
     > [!NOTE]
     > Jeśli grupa NSG jest stosowane tooonly pusty podsieci, maszyny wirtualne nie są wyświetlane. Jeśli grupa NSG jest stosowane tooa karty Sieciowej, która nie jest skojarzona z maszyną Wirtualną, te karty sieciowe również nie są wyświetlane. 
     > 
     > 
   * **Interfejs sieciowy:** maszyny Wirtualnej może mieć wiele interfejsów sieciowych. Możesz wybrać karty sieciowej dołączonych toohello wybrane maszyny Wirtualnej.
   * **AssociatedNSGs:** w dowolnym momencie, karta sieciowa może zawierać maksymalnie tootwo skuteczne grup NSG, jeden stosowane toohello karty Sieciowej i hello innych podsieci toohello. Mimo że hello zakres został wybrany jako grupa nsg VM1, jeśli hello karta sieciowa ma podsieć skuteczne NSG, hello dane wyjściowe będą pokazywały obu grup NSG.
4. Zasady można edytować bezpośrednio do grupy zabezpieczeń sieci skojarzonych z karty Sieciowej lub podsieci. jak to zrobić, przeczytaj toolearn krok 8 hello **wyświetlić reguły efektywnym elementem systemu zabezpieczeń dla maszyny wirtualnej** sekcji tego artykułu.

więcej informacji o toolearn hello dodatkowe informacje wyświetlane, przeczytaj kroku 6 hello **wyświetlić reguły efektywnym elementem systemu zabezpieczeń dla maszyny wirtualnej** sekcji tego artykułu.

> [!NOTE]
> Chociaż podsieci i karty Sieciowej można mieć tylko jeden toothem grupa NSG stosowana, grupy NSG mogą być skojarzone toomultiple kart sieciowych i wielu podsieci.
> 
> 

## <a name="considerations"></a>Zagadnienia do rozważenia
Należy wziąć pod uwagę następujące punkty podczas rozwiązywania problemów z łącznością hello:

* Reguły NSG domyślne zablokuje dostęp przychodzący do z hello internet i zezwolenia sieci wirtualnej ruch przychodzący. Zasady należy jawnie dodać tooallow ruchu przychodzącego dla dostępu z Internetu, zgodnie z potrzebami.
* Jeśli nie żadnych reguł zabezpieczeń grupy NSG powoduje toofail łączności sieciowej maszyny Wirtualnej, hello problem może być:
  * Oprogramowanie zapory w systemie operacyjnym hello maszyny Wirtualnej
  * Trasy skonfigurowanych dla urządzenia wirtualnego lub ruch lokalny. Ruch internetowy może być przekierowane tooon lokalnych przy użyciu tunelowania wymuszonego. Połączenia protokołu RDP/SSH z tooyour Internet hello maszyna wirtualna może nie działać to ustawienie, w zależności od tego, jak sprzętu sieciowego lokalne powitania obsługuje ten ruch. Odczyt hello [Rozwiązywanie problemów z tras](virtual-network-routes-troubleshoot-powershell.md) toolearn artykułu, jak toodiagnose trasy problemów, które mogą utrudnić hello przepływu ruchu w hello maszyny Wirtualnej. 
* Jeśli ma połączyć za pomocą sieci wirtualnych, domyślnie, hello VIRTUAL_NETWORK tag automatycznie rozwiń tooinclude prefiksy dla połączyć za pomocą sieci wirtualnych. Prefiksy te można wyświetlić w hello **ExpandedAddressPrefix** listy tootroubleshoot żadnych problemów powiązanych tooVNet równorzędna łączności. 
* Reguły efektywnym elementem systemu zabezpieczeń są wyświetlane tylko jeśli istnieje grupa NSG skojarzonego z hello maszyny Wirtualnej karty Sieciowej i podsieci. 
* Jeśli nie ma żadnych grup NSG skojarzone z hello karty Sieciowej lub w podsieci i publicznego adresu IP przypisany tooyour maszyna wirtualna, wszystkie porty jest otwarte dla przychodzący i wychodzący dostęp. Jeśli hello maszyna wirtualna ma publiczny adres IP, zdecydowanie zalecane jest stosowanie toohello grup NSG karty Sieciowej lub podsieci.

