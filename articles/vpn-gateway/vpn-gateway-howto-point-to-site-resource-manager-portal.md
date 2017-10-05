---
title: "Łączenie komputera z siecią wirtualną przy użyciu połączenia typu punkt-lokacja i uwierzytelniania certyfikatu: Azure Portal | Microsoft Docs"
description: "Bezpiecznie połącz komputer z siecią wirtualną platformy Azure przez utworzenie połączenia bramy sieci VPN typu punkt-lokacja przy użyciu uwierzytelniania certyfikatu. Ten artykuł ma zastosowanie w modelu wdrażania przy użyciu usługi Resource Manager i użyto w nim witryny Azure Portal."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 5c8e99f3ba52ef5d6f9f99ac24891c38e8970fff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-a-point-to-site-connection-to-a-vnet-using-certificate-authentication-azure-portal"></a>Konfigurowanie połączenia typu punkt-lokacja z siecią wirtualną przy użyciu uwierzytelniania certyfikatu: Azure Portal

W tym artykule pokazano sposób tworzenia sieci wirtualnej z połączeniem typu punkt-lokacja w modelu wdrażania przy użyciu usługi Resource Manager za pomocą witryny Azure Portal. Ta konfiguracja korzysta z certyfikatów do uwierzytelniania klienta nawiązującego połączenie. Tę konfigurację możesz również utworzyć przy użyciu innego narzędzia wdrażania lub modelu wdrażania, wybierając inną opcję z następującej listy:

> [!div class="op_single_selector"]
> * [Witryna Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal Azure (klasyczny)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Brama sieci VPN typu punkt-lokacja (P2S, Point-to-Site) pozwala utworzyć bezpieczne połączenie z siecią wirtualną z poziomu komputera klienckiego. Połączenia sieci VPN typu punkt-lokacja przydają się w przypadku, gdy celem użytkownika jest połączenie się z siecią wirtualną z lokalizacji zdalnej, podczas pracy zdalnej z domu lub konferencji. Połączenie sieci VPN typu punkt-lokacja jest również przydatne zamiast połączenia sieci VPN typu lokacja-lokacja w przypadku niewielkiej liczby klientów, którzy muszą się łączyć z siecią wirtualną. 

Połączenie typu punkt-lokacja używa protokołu SSTP (Secure Socket Tunneling Protocol), który jest protokołem sieci VPN opartym na protokole SSL. Połączenie sieci VPN typu punkt-lokacja jest nawiązywane przez zainicjowanie go z komputera klienckiego.

![Diagram: połączenie typu punkt-lokacja](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

Połączenia typu punkt-lokacja z uwierzytelnianiem certyfikatu mają następujące wymagania:

* Brama sieci VPN oparta na trasie.
* Klucz publiczny (plik cer) dla certyfikatu głównego, przekazany na platformę Azure. Przekazany certyfikat jest uznawany za certyfikat zaufany i używany do uwierzytelniania.
* Certyfikat klienta wygenerowany na podstawie certyfikatu głównego i zainstalowany na każdym komputerze klienckim, który będzie nawiązywać połączenie z siecią wirtualną. Ten certyfikat jest używany do uwierzytelniania klientów.
* Pakiet konfiguracji klienta sieci VPN. Pakiet konfiguracji klienta sieci VPN zawiera informacje potrzebne klientowi do nawiązania połączenia z siecią wirtualną. Pakiet konfiguruje istniejącego klienta sieci VPN, który jest natywnym klientem systemu operacyjnego Windows. Każdy klient, który nawiązuje połączenie, musi być skonfigurowany przy użyciu pakietu konfiguracji.

Połączenia typu punkt-lokacja nie wymagają urządzenia sieci VPN ani lokalnego publicznego adresu IP. Połączenie sieci VPN jest nawiązywane za pośrednictwem protokołu SSTP (Secure Socket Tunneling Protocol). Po stronie serwera obsługiwany jest protokół SSTP w wersji 1.0, 1.1 i 1.2. Klient decyduje o wyborze wersji do użycia. W przypadku systemu Windows 8.1 i nowszych protokół SSTP domyślnie używa wersji 1.2.

Więcej informacji na temat połączeń typu punkt-lokacja znajduje się w sekcji [Często zadawane pytania dotyczące połączeń typu punkt-lokacja](#faq) na końcu tego artykułu.

#### <a name="example"></a>Przykładowe wartości

Następujących wartości możesz użyć do tworzenia środowiska testowego lub odwoływać się do tych wartości, aby lepiej zrozumieć przykłady w niniejszym artykule:

* **Nazwa sieci wirtualnej:** VNet1
* **Przestrzeń adresowa:** 192.168.0.0/16<br>W tym przykładzie zostanie wykorzystana tylko jedna przestrzeń adresowa. Istnieje możliwość użycia więcej niż jednej przestrzeni adresowej dla sieci wirtualnej.
* **Nazwa podsieci:** FrontEnd
* **Zakres adresów podsieci:** 192.168.1.0/24
* **Subskrypcja:** jeśli masz więcej niż jedną subskrypcję, sprawdź, czy korzystasz z właściwej.
* **Grupa zasobów:** TestRG
* **Lokalizacja:** Wschodnie stany USA
* **GatewaySubnet:** 192.168.200.0/24<br>
* **Serwer DNS:** (opcjonalny) adres IP serwera DNS, który ma być używany do rozpoznawania nazw.
* **Nazwa bramy sieci wirtualnej:** VNet1GW
* **Typ bramy:** VPN
* **Typ sieci VPN:** oparta na trasach
* **Publiczny adres IP:** VNet1GWpip
* **Typ połączenia:** Punkt-lokacja
* **Pula adresów klienta:** 172.16.201.0/24<br>Klienci sieci VPN połączeni z siecią wirtualną, którzy korzystają z tego połączenia punkt-lokacja, otrzymują adresy IP z puli adresów klientów.

## <a name="createvnet"></a>1. Tworzenie sieci wirtualnej

Przed rozpoczęciem sprawdź, czy masz subskrypcję platformy Azure. Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz aktywować [korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) lub utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial).

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Dodawanie podsieci bramy

Przed połączeniem sieci wirtualnej z bramą należy najpierw utworzyć podsieć bramy sieci wirtualnej, z którą ma zostać nawiązane połączenie. Usługi bramy korzystają z adresów IP określonych w podsieci bramy. Jeśli to możliwe, utwórz podsieć bramy przy użyciu bloku CIDR /28 lub /27 w celu zapewnienia wystarczającej liczby adresów IP, aby uwzględnić wymagania dotyczące dodatkowych przyszłych konfiguracji.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. Określanie serwera DNS (opcjonalne)

Po utworzeniu sieci wirtualnej możesz dodać adres IP serwera DNS, aby umożliwić obsługę rozpoznawania nazw. Serwer DNS jest opcjonalny w przypadku tej konfiguracji, ale jest wymagany, jeśli chcesz korzystać z rozpoznawania nazw. Określenie wartości nie powoduje utworzenia nowego serwera DNS. Określony adres IP serwera DNS powinien być adresem serwera będącego w stanie rozpoznawać nazwy zasobów, z którymi nawiązywane jest połączenie. W tym przykładzie użyto prywatnego adresu IP, ale może to nie być adres IP Twojego serwera DNS. Pamiętaj, aby użyć własnych wartości.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. Tworzenie bramy sieci wirtualnej

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. Generowanie certyfikatów klienta

Certyfikaty są używane przez platformę Azure do uwierzytelniania klientów łączących się z siecią wirtualną za pośrednictwem połączenia sieci VPN typu punkt-lokacja. Po uzyskaniu certyfikatu głównego należy [przekazać](#uploadfile) informacje o kluczu publicznym do platformy Azure. Certyfikat główny jest następnie uznawany przez platformę Azure za zaufany dla połączeń typu punkt-lokacja z siecią wirtualną. Ponadto certyfikaty klienta są generowane na podstawie zaufanego certyfikatu głównego, a następnie instalowane na każdym komputerze klienckim. Certyfikat klienta jest używany do uwierzytelniania klienta, gdy inicjuje on połączenie z siecią wirtualną. 

### <a name="getcer"></a>1. Uzyskiwanie pliku cer dla certyfikatu głównego

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. Generowanie certyfikatu klienta

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Dodawanie puli adresów klienta

Pula adresów klienta to określony przez Ciebie zakres prywatnych adresów IP. Klienci łączący się przez połączenie VPN typu punkt-lokacja otrzymują adres IP z tego zakresu. Używaj zakresu prywatnych adresów IP nienakładającego się na lokalizację lokalną, z której się łączysz, ani na sieć wirtualną, z którą chcesz się łączyć.

1. Po utworzeniu bramy sieci wirtualnej przejdź do sekcji **Ustawienia** na stronie bramy sieci wirtualnej. W sekcji **Ustawienia** kliknij pozycję **Konfiguracja punktu do lokacji**, aby otworzyć stronę **Konfiguracja punktu do lokacji**.

  ![Strona połączenia typu punkt-lokacja](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. Na stronie **Konfiguracja punktu do lokacji** możesz usunąć automatycznie wypełniony zakres, a następnie dodać zakres prywatnych adresów IP, z którego chcesz korzystać. Kliknij pozycję **Zapisz**, aby zweryfikować i zapisać ustawienie.

  ![Pula adresów klienta](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Przekazywanie danych certyfikatu publicznego dla certyfikatu głównego

Po utworzeniu bramy możesz przekazać do platformy Azure informacje o kluczu publicznym dla certyfikatu głównego. Po przekazaniu danych certyfikatu publicznego platforma Azure może używać go do uwierzytelniania klientów, którzy mają zainstalowany certyfikat klienta wygenerowany na podstawie zaufanego certyfikatu głównego. Możesz przekazać łącznie do 20 zaufanych certyfikatów głównych.

1. Certyfikaty są dodawane na stronie **Konfiguracja punktu do lokacji** w sekcji **Certyfikat główny**.  
2. Upewnij się, że certyfikat główny został wyeksportowany jako plik X.509 (cer) zaszyfrowany z użyciem algorytmu Base-64. Certyfikat należy wyeksportować w takim formacie, aby możliwe było jego otwarcie za pomocą edytora tekstów.
3. Otwórz certyfikat za pomocą edytora tekstów, takiego jak Notatnik. Podczas kopiowania danych dotyczących certyfikatu upewnij się, że kopiujesz tekst jako jeden ciągły wiersz bez znaków powrotu karetki i wysuwu wiersza. Może zajść potrzeba zmodyfikowania widoku w edytorze tekstu na potrzeby pokazywania symboli lub pokazywania wszystkich znaków, aby wyświetlić znaki powrotu karetki i wysuwu wiersza. Skopiuj tylko następującą sekcję jako jeden ciągły wiersz:

  ![Dane dotyczące certyfikatu](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Wklej dane dotyczące certyfikatu w polu **Dane certyfikatu publicznego**. Korzystając z pola **Nazwa**, określ nazwę certyfikatu, a następnie kliknij przycisk **Zapisz**. Możesz dodać maksymalnie 20 zaufanych certyfikatów głównych.

  ![Przekazywanie certyfikatu](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. Generowanie i instalowanie pakietu konfiguracji klienta sieci VPN

Aby można było nawiązać połączenie z siecią wirtualną przy użyciu połączenia VPN typu punkt-lokacja, na każdym kliencie musi być zainstalowany pakiet konfiguracji klienta, który konfiguruje natywnego klienta sieci VPN przy użyciu ustawień i plików wymaganych do połączenia z siecią wirtualną. Pakiet konfiguracji klienta sieci VPN konfiguruje natywnego klienta sieci VPN systemu Windows. Nie instaluje on nowego ani innego klienta sieci VPN.

Tego samego pakietu konfiguracji klienta VPN można użyć na każdym komputerze klienckim, o ile wersja jest zgodna z architekturą dla klienta. Lista obsługiwanych systemów operacyjnych klienta znajduje się w sekcji [Często zadawane pytania dotyczące połączeń typu punkt-lokacja](#faq) na końcu tego artykułu.

### <a name="step-1---generate-and-download-the-client-configuration-package"></a>Krok 1 — Generowanie i pobieranie pakietu konfiguracji klienta

1. Na stronie **Konfiguracja punktu do lokacji** kliknij przycisk **Download VPN client** (Pobierz klienta sieci VPN), aby otworzyć stronę **Download VPN client** (Pobieranie klienta sieci VPN). Wygenerowanie pakietu trwa minutę lub dwie.

  ![Pobieranie klienta VPN — sposób 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. Wybierz właściwy pakiet dla klienta, a następnie kliknij przycisk **Pobierz**. Zapisz plik pakietu konfiguracji. Pakiet konfiguracji klienta VPN należy zainstalować na każdym komputerze klienckim, który łączy się z siecią wirtualną.

  ![Pobieranie klienta VPN — sposób 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-the-client-configuration-package"></a>Krok 2 — Instalowanie pakietu konfiguracji klienta

1. Skopiuj lokalnie plik konfiguracji na komputer, który chcesz połączyć z siecią wirtualną. 
2. Kliknij dwukrotnie plik exe, aby zainstalować pakiet na komputerze klienckim. Ponieważ pakiet konfiguracji został utworzony przez Ciebie, nie jest podpisany i może zostać wyświetlone ostrzeżenie. Jeśli pojawi się okno podręczne Windows SmartScreen, kliknij pozycję **Więcej informacji** (z lewej strony), a następnie pozycję **Uruchom mimo to**, aby zainstalować pakiet.
3. Zainstaluj pakiet na komputerze klienckim. Jeśli pojawi się okno podręczne Windows SmartScreen, kliknij pozycję **Więcej informacji** (z lewej strony), a następnie pozycję **Uruchom mimo to**, aby zainstalować pakiet.
4. Na komputerze klienckim przejdź do obszaru **Ustawienia sieci** i kliknij pozycję **Sieć VPN**. Połączenie z siecią VPN zawiera nazwę sieci wirtualnej, z którą jest nawiązywane połączenie.

## <a name="installclientcert"></a>9. Instalowanie wyeksportowanego certyfikatu klienta

Jeśli chcesz utworzyć połączenie punkt-lokacja z komputerem klienckim innym niż użyty do wygenerowania certyfikatów klienta, należy zainstalować certyfikat klienta. Podczas instalowania certyfikatu klienta potrzebne jest hasło, które zostało utworzone w trakcie eksportowania certyfikatu klienta. Zazwyczaj jest to kwestia dwukrotnego kliknięcia certyfikatu i zainstalowania go.

Upewnij się, że certyfikat klienta został wyeksportowany jako plik pfx wraz z całym łańcuchem certyfikatów (jest to ustawienie domyślne). W przeciwnym razie informacje o certyfikacie głównym nie będą dostępne na komputerze klienckim i klient nie będzie mógł się poprawnie uwierzytelnić. Aby uzyskać więcej informacji, zobacz [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install) (Instalowanie wyeksportowanego certyfikatu klienta).

## <a name="connect"></a>10. Nawiązywanie połączenia z usługą Azure

1. Aby nawiązać połączenie z siecią wirtualną na komputerze klienckim, przejdź do połączeń sieci VPN i wyszukaj wcześniej utworzone połączenie sieci VPN. Połączenie będzie miało taką samą nazwę jak sieć wirtualna. Kliknij przycisk **Połącz**. Może pojawić się komunikat podręczny, który odwołuje się do użycia certyfikatu. Kliknij przycisk **Kontynuuj**, aby skorzystać z podwyższonego poziomu uprawnień.

2. Na stronie stanu **Połączenie** kliknij przycisk **Połącz**, aby rozpocząć połączenie. Jeśli widzisz ekran **Wybierz certyfikat**, sprawdź, czy wyświetlany certyfikat klienta to ten, który ma zostać użyty do nawiązania połączenia. Jeśli nie, kliknij strzałkę na liście rozwijanej, aby wybrać właściwy certyfikat, a następnie kliknij przycisk **OK**.

  ![Łączenie klienta sieci VPN z platformą Azure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. Połączenie zostało ustanowione.

  ![Ustanowiono połączenie](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Rozwiązywanie problemów dotyczących połączeń typu punkt-lokacja

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. Weryfikowanie połączenia

1. Aby sprawdzić, czy połączenie sieci VPN jest aktywne, otwórz wiersz polecenia z podwyższonym poziomem uprawnień, a następnie uruchom polecenie *ipconfig/all*.
2. Przejrzyj wyniki. Zwróć uwagę na fakt, że otrzymany adres IP należy do określonej podczas konfiguracji połączenia punkt-lokacja puli adresów klienta sieci VPN. Wyniki są podobne, jak w następującym przykładzie:

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Nawiązywanie połączenia z maszyną wirtualną

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>Dodawanie lub usuwanie zaufanych certyfikatów głównych

Zaufane certyfikaty główne można dodawać do platformy Azure lub z niej usuwać. Po usunięciu certyfikatu głównego klienci, którzy mają certyfikat wygenerowany na podstawie tego certyfikatu głównego, nie będą w stanie się uwierzytelnić i w związku z tym nie będą mogli nawiązywać połączeń. Jeśli chcesz, aby klienci mogli uwierzytelniać się i nawiązywać połączenia, musisz zainstalować nowy certyfikat klienta wygenerowany na podstawie certyfikatu głównego, który jest traktowany jako zaufany przez platformę Azure (przekazany na tę platformę).

### <a name="to-add-a-trusted-root-certificate"></a>Aby dodać zaufany certyfikat główny

Na platformie Azure można dodać maksymalnie 20 plików cer zaufanego certyfikatu głównego. Aby uzyskać instrukcje, zobacz sekcję [Przekazywanie zaufanego certyfikatu głównego](#uploadfile) w tym artykule.

### <a name="to-remove-a-trusted-root-certificate"></a>Usuwanie zaufanego certyfikatu głównego

1. Aby usunąć zaufany certyfikat główny, przejdź do strony **Konfiguracja punktu do lokacji** dla bramy Twojej sieci wirtualnej.
2. W sekcji **Certyfikat główny** na stronie znajdź certyfikat, który chcesz usunąć.
3. Kliknij wielokropek obok certyfikatu, a następnie kliknij pozycję „Usuń”.

## <a name="revokeclient"></a>Odwoływanie certyfikatu klienta

Certyfikaty klienta można odwołać. Lista odwołania certyfikatów umożliwia dokonanie selektywnej odmowy połączenia punkt-lokacja w oparciu o indywidualne certyfikaty klienta. Różni się to od usuwania zaufanego certyfikatu głównego. Jeśli usuniesz plik cer zaufanego certyfikatu głównego z platformy Azure, spowoduje to odwołanie dostępu dla wszystkich certyfikatów klienta wygenerowanych lub podpisanych przez odwołany certyfikat główny. Odwołanie certyfikatu klienta zamiast certyfikatu głównego pozwala dalej używać innych certyfikatów wygenerowanych na podstawie certyfikatu głównego do uwierzytelniania.

Częstą praktyką jest użycie certyfikatu głównego do zarządzania dostępem na poziomach zespołu lub organizacji przy jednoczesnym korzystaniu z odwołanych certyfikatów klienta dla bardziej precyzyjnej kontroli dostępu poszczególnych użytkowników.

### <a name="to-revoke-a-client-certificate"></a>Aby odwołać certyfikat klienta

Certyfikat klienta można odwołać przez dodanie odcisku palca do listy odwołania.

1. Pobierz odcisk palca certyfikatu klienta. Aby uzyskać więcej informacji, zobacz [Jak pobrać odcisk palca certyfikatu](https://msdn.microsoft.com/library/ms734695.aspx).
2. Skopiuj informacje do edytora tekstu i usuń wszelkie spacje, tak aby powstał ciąg bez odstępów.
3. Przejdź do strony **Konfiguracja punktu do lokacji** bramy sieci wirtualnej. Korzystając z tej samej strony, [przekazano zaufany certyfikat główny](#uploadfile).
4. W sekcji **Odwołane certyfikaty** wprowadź przyjazną nazwę certyfikatu (nie musi to być nazwa pospolita certyfikatu).
5. Skopiuj i wklej ciąg odcisku palca do pola **Odcisk palca**.
6. Odcisk palca zostanie zweryfikowany i automatycznie dodany do listy odwołania. Na ekranie zobaczysz komunikat informujący o aktualizowaniu listy. 
7. Po zakończeniu aktualizowania nie będzie można już używać certyfikatu do nawiązywania połączeń. Klienci, którzy spróbują połączyć się za pomocą tego certyfikatu, zobaczą komunikat informujący o tym, że certyfikat nie jest już ważny.

## <a name="faq"></a>Często zadawane pytania dotyczące połączeń typu punkt-lokacja

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Następne kroki
Po zakończeniu procesu nawiązywania połączenia można dodać do sieci wirtualnych maszyny wirtualne. Aby uzyskać więcej informacji, zobacz [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) (Maszyny wirtualne). Aby dowiedzieć się więcej o sieci i maszynach wirtualnych, zobacz [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md) (Omówienie sieci maszyny wirtualnej z systemem Linux i platformy Azure).