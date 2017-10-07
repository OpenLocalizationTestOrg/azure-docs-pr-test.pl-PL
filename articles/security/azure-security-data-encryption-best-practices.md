---
title: "aaaData zabezpieczeń i najlepsze rozwiązania w zakresie szyfrowania | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera zestaw najlepsze rozwiązania dotyczące bezpieczeństwa danych i szyfrowania za pomocą wbudowanych funkcji platformy Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 17ba67ad-e5cd-4a8f-b435-5218df753ca4
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: 5057c85ed3107921462a40045e716675ea41e4bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-security-and-encryption-best-practices"></a>Dobre praktyki dotyczące zabezpieczeń danych platformy Azure i szyfrowania
Jeden z ochrony toodata klucze hello w chmurze hello jest księgowanie hello możliwe stany, w których może wystąpić danych oraz kontrolki są dostępne dla tego stanu. Najlepsze praktyki dotyczące danych Azure zabezpieczeń i szyfrowania w celu hello hello zalecenia będą wokół hello następujące stany danych:

* W pozostałych: W tym wszystkie informacje, które typy, statycznie występujących na nośnik fizyczny, kontenerów i obiektów magazynu można go magnetyczne lub optyczne dysku.
* Podczas przesyłania: Podczas transferu danych między składnikami, lokalizacji lub programy, takie jak sieci hello przez usługi service bus (z toocloud lokalnie i na odwrót, łącznie z połączeń hybrydowych, takich jak usługi ExpressRoute), lub w trakcie operacji We/Wy proces, jego jest traktować jako w ruchu.

W tym artykule omówiono kolekcji danych Azure zabezpieczeń i szyfrowania najlepszych rozwiązań. Następujące najlepsze rozwiązania są uzyskiwane z wiemy z doświadczenia z zabezpieczeniami danych Azure oraz szyfrowania i hello wrażenia klientów, takie jak samodzielnie.

Dla każdego ze względów wyjaśniamy:

* Jakie hello najlepszym rozwiązaniem jest
* Dlaczego chcesz tooenable tej najlepsze praktyki
* Co może wynikać hello tooenable hello najlepszym rozwiązaniem w przeciwnym przypadku
* Najlepszym rozwiązaniem toohello możliwe alternatywy
* Jak można znaleźć tooenable hello najlepsze praktyki

W tym artykule Azure bezpieczeństwo danych i najlepsze rozwiązania w zakresie szyfrowania jest na podstawie opinii konsensu i funkcji platformy Azure i zestawy funkcji istniejących w chwili hello, który został zapisany w tym artykule. Opinie i technologie ulegną zmianom i będą w tym artykule zaktualizowane na tooreflect regularnie tych zmian.

Danych Azure szyfrowania najlepsze praktyki dotyczące zabezpieczeń i omówione w tym artykule obejmują:

* Wymusić uwierzytelnianie wieloskładnikowe
* Kontrola dostępu (RBAC) oparta na rolach użycia
* Szyfrowanie maszyn wirtualnych platformy Azure
* Używanie modeli zabezpieczeń sprzętu
* Zarządzanie za pomocą bezpiecznego stacji roboczych
* Włącz szyfrowanie danych SQL
* Ochrona danych podczas przesyłania
* Wymuszanie szyfrowania danych na poziomie plików

## <a name="enforce-multi-factor-authentication"></a>Wymusić uwierzytelnianie wieloskładnikowe
Hello pierwszym etapem dostęp do danych i sterowania w programie Microsoft Azure jest tooauthenticate hello użytkownika. [Usługa Azure Multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md) jest metodą weryfikacji tożsamości użytkownika przy użyciu innej metody niż tylko nazwę użytkownika i hasło. Ta metoda uwierzytelniania ułatwia zabezpieczenie dostępu toodata i aplikacje spełniając zapotrzebowanie na prosty proces logowania.

Włączanie usługi Azure MFA dla użytkowników, dodajesz drugą warstwę logowania toouser zabezpieczeń i transakcji. W takim przypadku transakcji może uzyskiwać dostęp do dokumentu znajdującego się na serwerze plików lub w trybie Online programu SharePoint. Usługa Azure MFA pomaga również IT tooreduce hello prawdopodobieństwo, że przejęciem poświadczeń tooorganization dostępu do danych.

Na przykład: Wymuszanie usługi Azure MFA dla użytkowników i skonfigurować go toouse Rozmowa telefoniczna lub wiadomości SMS jako weryfikacji, w przypadku złamania zabezpieczeń poświadczeń użytkownika hello, osoba atakująca hello nie być możliwe tooaccess dowolnego zasobu, ponieważ on nie będą miały dostępu toouser telefonu. Organizacje, które nie dodawaj tego dodatkową warstwę ochrony tożsamości są bardziej narażony na atak kradzieży poświadczeń, co może prowadzić do naruszenia toodata.

Jeden alternatywą dla organizacji, które mają kontrola uwierzytelniania hello tookeep lokalnej jest toouse [serwera usługi Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), nazywany również lokalne usługi MFA. Za pomocą tej metody będą mogli tooenforce uwierzytelnianie wieloskładnikowe, przy zachowaniu hello MFA serwera lokalnego.

Aby uzyskać więcej informacji dotyczących usługi Azure MFA, przeczytaj artykuł hello [wprowadzenie do korzystania z usługi Azure Multi-Factor Authentication w chmurze hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Kontrola dostępu (RBAC) oparta na rolach użycia
Ograniczanie dostępu oparte na powitania [muszą tooknow](https://en.wikipedia.org/wiki/Need_to_know) i [najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege) zasad zabezpieczeń. Jest to konieczne w przypadku organizacji, które mają tooenforce zasad zabezpieczeń dla dostępu do danych. Azure opartej na rolach kontroli dostępu (RBAC) może być używane tooassign toousers uprawnienia, grup i aplikacji w zakresie niektórych. Witaj zakres przypisania roli może być pojedynczego zasobu, grupy zasobów lub subskrypcji.

Można wykorzystać [wbudowane role RBAC](../active-directory/role-based-access-built-in-roles.md) na platformie Azure tooassign uprawnienia toousers. Należy rozważyć użycie *współautora konta magazynu* dla operatorów chmury, które wymagają konta magazynu toomanage i *klasycznego współautora konta magazynu* roli toomanage klasycznych kont magazynu. Operatorom chmury, które musi toomanage maszyn wirtualnych i konto magazynu, należy rozważyć dodanie ich zbyt*Współautor·maszyny·wirtualnej* roli.

Organizacje, które nie wymusić kontrolę dostępu danych dzięki wykorzystaniu możliwości, takie jak RBAC może nadanie więcej uprawnień niż jest to niezbędne dla użytkowników. Może to spowodować naruszenie toodata przez niektórych użytkowników mających toodata dostępu, którego nie ma w miejscu pierwszego hello.

Użytkownik może dowiedzieć się więcej o Azure RBAC od przeczytania artykułu hello [kontroli dostępu](../active-directory/role-based-access-control-configure.md).

## <a name="encrypt-azure-virtual-machines"></a>Szyfrowanie maszyn wirtualnych platformy Azure
W przypadku wielu organizacji [szyfrowanie danych magazynowanych](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) jest obowiązkowy krok na drodze suwerenności dane, zgodności i ochrony prywatności danych. Szyfrowanie dysków Azure umożliwia tooencrypt Administratorzy IT systemu Windows i Linux IaaS maszyn wirtualnych (VM) dysków. Szyfrowanie dysków Azure wykorzystuje hello branżowy standard funkcji BitLocker funkcji systemu Windows i DM-Crypt hello funkcji szyfrowania woluminów tooprovide Linux hello systemu operacyjnego i dysków danych hello.

Można korzystać z szyfrowania dysków Azure toohelp ochrony i chronić Twoje dane toomeet wymagań organizacyjnych zabezpieczeń i zgodności. Organizacje powinny również należy rozważyć włączenie szyfrowania toohelp ograniczyć dostęp do danych powiązanych toounauthorized ryzyka. Zalecane jest również szyfrowanie toothem poufnych danych przed toowriting dysków.

Upewnij się, że tooencrypt woluminów danych maszyny Wirtualnej i woluminu rozruchowego w kolejności tooprotect dane przechowywane na koncie magazynu Azure. Zabezpieczenia hello szyfrowania kluczy i kluczy tajnych dzięki wykorzystaniu [usługi Azure Key Vault](../key-vault/key-vault-whatis.md).

Dla lokalnych serwerów systemu Windows należy wziąć pod uwagę następujące najlepsze rozwiązania w zakresie szyfrowania hello:

* Użyj [funkcji BitLocker](https://technet.microsoft.com/library/dn306081.aspx) do szyfrowania danych
* Przechowuje informacje dotyczące odzyskiwania w usługach AD DS.
* W przypadku jakiekolwiek wątpliwości, że został złamany klucze funkcji BitLocker, zaleca się albo format hello dysku tooremove wszystkich wystąpień hello metadanych funkcji BitLocker z dysku hello lub odszyfrować i ponownie szyfrować cały dysk hello.

Organizacje, które nie wymuszania szyfrowania danych są bardziej prawdopodobne toodata toobe widoczne problemy z integralnością, takich jak użytkownicy złośliwego lub nieautoryzowane kradzieży danych i naruszenia zabezpieczeń kont uzyskania nieautoryzowanego dostępu toodata w formacie zwykłego. Oprócz tych zagrożeń firm, które mają toocomply z przepisów branżowych dowieść są większego i korzystają z hello poprawne formanty tooenhance danych zabezpieczeń.

Użytkownik może dowiedzieć się więcej o szyfrowania dysków Azure od przeczytania artykułu hello [Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS](azure-security-disk-encryption.md).

## <a name="use-hardware-security-modules"></a>Użyj sprzętowych modułów zabezpieczeń
Rozwiązania szyfrowania zgodne ze standardami używają kluczy tajnych tooencrypt danych. W związku z tym jest krytyczny, że te klucze są bezpiecznie przechowywane. Zarządzanie kluczami staje się integralną częścią ochrony danych, ponieważ będzie ona wykorzystywana toostore klucze tajne, które są używane tooencrypt danych.

Używa szyfrowania dysków Azure [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) toohelp podczas sterowania i zarządzania nimi klucze szyfrowania dysku i kluczy tajnych w ramach subskrypcji magazynu kluczy, zapewniając, że wszystkie dane w hello dysków maszyny wirtualnej są szyfrowane, gdy w platformy Azure Magazyn. Należy używać usługi Azure Key Vault tooaudit kluczy i użycia zasad.

Istnieje wiele toonot powiązany ryzykiem posiadające odpowiednie środki zabezpieczające w miejscu tooprotect hello klucze tajne, które były używane tooencrypt danych. Jeśli atakujący ma dostęp do kluczy tajnych toohello, one będą mogli toodecrypt hello danych i mogących mieć dostęp do informacji tooconfidential.

Użytkownik może dowiedzieć się więcej o ogólne zalecenia dotyczące zarządzania certyfikatami w usłudze Azure od przeczytania artykułu hello [zarządzania certyfikatami w usłudze Azure: porady](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/).

Aby uzyskać więcej informacji na temat usługi Azure Key Vault, przeczytaj [wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md).

## <a name="manage-with-secure-workstations"></a>Zarządzanie za pomocą bezpiecznego stacji roboczych
Od hello większość użytkownika końcowego hello hello ataków docelowych punktu końcowego hello staje się jednego z punktów głównej hello ataku. Jeśli osoba atakująca obniża hello punktu końcowego, on mogą korzystać z danych użytkownika hello poświadczenia toogain dostępu tooorganization firmy. Większość ataków punktu końcowego są możliwe tootake zaletą hello fakt, że użytkownicy końcowi są administratorami w swoich lokalnych stacji roboczych.

Aby zmniejszyć to ryzyko, należy za pomocą bezpiecznego zarządzania stacji roboczej. Firma Microsoft zaleca użycie [uprzywilejowanego dostępu do stacji roboczych (ŁAPY)](https://technet.microsoft.com/library/mt634654.aspx) tooreduce hello ataku w stacji roboczych. Te stacje robocze bezpiecznego zarządzania mogą pomóc ograniczyć niektóre z nich ataków zapewnienia Twoje dane są bezpieczniejsze. Upewnij się toouse ŁAPY tooharden i blokady w dół stacji roboczej. Jest to ważny krok tooprovide wysokiego poziomu zabezpieczeń gwarancji dla kont poufnych, zadania i ochrony danych.

Brak programu endpoint protection może zagrożenie danych, upewnij się, że tooenforce zasad zabezpieczeń dla wszystkich urządzeń, które są używane tooconsume danych, bez względu na lokalizację danych hello (chmurze lub lokalnie).

Dowiedz się więcej o uprawnieniach dostępu stacji roboczej od przeczytania artykułu hello [zabezpieczanie uprzywilejowanego dostępu](https://technet.microsoft.com/library/mt631194.aspx).

## <a name="enable-sql-data-encryption"></a>Włącz szyfrowanie danych SQL
[Azure SQL Database przezroczystego szyfrowania danych](https://msdn.microsoft.com/library/dn948096.aspx) (funkcji TDE) ułatwia ochronę przed zagrożeniem hello złośliwych działań, wykonując w czasie rzeczywistym szyfrowania i odszyfrowywania hello bazy danych, skojarzonych kopii zapasowych, i pliki dziennika transakcji w stanie spoczynku bez Aplikacja toohello wymagające zmiany.  Funkcji TDE szyfruje magazyn hello całej bazy danych przy użyciu klucza szyfrowania symetrycznego klucza o nazwie hello bazy danych.

Nawet wtedy, gdy cały magazyn hello jest zaszyfrowany, bardzo ważne jest tooalso szyfrowania bazy danych sam. Jest to implementacja obrony hello w głębokość podejście do ochrony danych. Jeśli używasz [bazy danych SQL Azure](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx) i chcesz, aby dane poufne tooprotect np. kart kredytowych lub numerów ubezpieczenia społecznego, można zaszyfrować baz danych z trybem FIPS 140-2 zweryfikowanych 256 bitowe szyfrowanie AES spełniające wymagania hello wielu standardy branżowe (np. HIPAA, PCI).

Jest ważne toounderstand, które pliki są powiązane za[rozszerzenia puli bufora](https://msdn.microsoft.com/library/dn133176.aspx) (BPE) nie są szyfrowane, gdy baza danych jest szyfrowana przy użyciu funkcji TDE. Należy użyć narzędzia szyfrowania na poziomie systemu plików, takich jak BitLocker lub hello [systemu szyfrowania plików](https://technet.microsoft.com/library/cc700811.aspx) (EFS) dla BPE powiązane pliki.

Od autoryzowanym użytkownikiem, takie jak administrator zabezpieczeń lub administrator bazy danych można uzyskiwać dostęp do danych hello nawet jeśli hello bazy danych jest szyfrowany przy funkcji TDE, należy również wykonać poniższe zalecenia hello:

* Uwierzytelnianie SQL na poziomie bazy danych hello
* Uwierzytelniania systemu Azure AD przy użyciu role RBAC
* Użytkownicy i aplikacje powinny używać tooauthenticate osobnych kont. W ten sposób można ograniczyć uprawnienia hello toousers i aplikacje i zmniejszenia ryzyka hello złośliwych działań
* Implementowanie zabezpieczeń na poziomie bazy danych przy użyciu ról stałej bazy danych (takich jak db_datareader lub db_datawriter), lub można tworzyć role niestandardowe dla twojej aplikacji toogrant obiektów bazy danych tooselected jawnych uprawnień

Organizacje, które nie używają szyfrowania na poziomie bazy danych może być bardziej narażony na ataki, które mogą negatywnie wpłynąć na danych znajdujących się w bazach danych SQL.

Możesz można dowiedzieć się więcej o funkcji SQL TDE szyfrowania od przeczytania artykułu hello [przezroczystego szyfrowania danych z bazy danych SQL Azure](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx).

## <a name="protect-data-in-transit"></a>Ochrona danych podczas przesyłania
Ochrona danych podczas przesyłania powinien być integralną część strategii ochrony danych. Ponieważ dane będą przenoszone i z powrotem w wielu lokalizacjach, ogólne zalecenie hello jest zawsze używaj danych tooexchange protokołów SSL/TLS w różnych lokalizacjach. W niektórych sytuacjach może być tooisolate hello całej komunikacji kanału między lokalnymi i w chmurze infrastruktury przy użyciu wirtualnej sieci prywatnej (VPN).

Przenoszenie między lokalną infrastrukturą i Azure danych należy rozważyć odpowiednie zabezpieczenia, takie jak HTTPS lub sieci VPN.

Dla organizacji, które wymagają dostępu toosecure z wielu stacjach roboczych znajdujących się lokalnie tooAzure, użyj [Azure VPN lokacja lokacja](../vpn-gateway/vpn-gateway-site-to-site-create.md).

Dla organizacji, które wymagają dostępu toosecure z jednej stacji roboczej znajdujących się lokalnie tooAzure, użyj [punkt-lokacja sieci VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md).

Większych zestawów danych można przenieść za pośrednictwem dedykowanej o dużej szybkości łącza sieci WAN takich jak [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Jeśli wybierzesz toouse ExpressRoute, można również szyfrowanie danych hello przy użyciu poziomu aplikacji hello [SSL/TLS](https://support.microsoft.com/kb/257591) lub innymi protokołami zapewnia dodatkową ochronę.

Jeśli użytkownik korzysta z usługi Azure Storage za pomocą portalu Azure hello, wszystkich transakcji jest realizowana za pośrednictwem protokołu HTTPS. [Interfejs API REST magazynu](https://msdn.microsoft.com/library/azure/dd179355.aspx) za pośrednictwem protokołu HTTPS może być również używane toointeract z [usługi Azure Storage](https://azure.microsoft.com/services/storage/) i [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/).

Organizacje, które nie są przesyłane dane tooprotect są bardziej narażony na [ataków man-in--middle](https://technet.microsoft.com/library/gg195821.aspx), [podsłuchiwaniu](https://technet.microsoft.com/library/gg195641.aspx) i przejęcie kontroli sesji. Tego rodzaju ataki może być pierwszym krokiem hello w uzyskiwaniu dostępu do danych tooconfidential.

Możesz można dowiedzieć się więcej o sieci VPN platformy Azure opcja od przeczytania artykułu hello [planowania i projektowania dla bramy sieci VPN](../vpn-gateway/vpn-gateway-plan-design.md).

## <a name="enforce-file-level-data-encryption"></a>Wymuszanie szyfrowania danych na poziomie plików
Szyfruje hello samym pliku, bez względu na lokalizację pliku hello kolejną warstwę ochrony, która może zwiększyć poziom hello zabezpieczeń danych.

[Usługa Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp zasad szyfrowania, tożsamości i autoryzacji używa Zabezpieczanie plików i wiadomości e-mail. Usługa Azure RMS działa na wielu urządzeniach — telefonach, tablety i komputery, aby chronić w obrębie organizacji i poza organizacją. Ta funkcja jest możliwa, ponieważ usługa Azure RMS dodaje poziom ochrony, który pozostaje hello danych, nawet wtedy, gdy opuszczą teren organizacji.

Gdy używasz usługi Azure RMS tooprotect plików za pomocą branżowego standardu kryptografii pełnej obsługi [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Podczas ochrony danych należy korzystać z usługi Azure RMS, masz hello gwarantują, że ochrona powitalnych pozostanie z plikiem hello, nawet jeśli jest skopiowany toostorage, który nie jest pod kontrolą hello IT, takich jak Usługa magazynu w chmurze. Hello sam występuje w przypadku plików udostępnianych za pośrednictwem poczty e-mail, hello plik jest chroniony jako załącznik tooan wiadomość e-mail, jak z instrukcjami tooopen hello chronionego załącznika.

Podczas planowania wdrożenia usługi Azure RMS firma Microsoft zaleca hello następujące czynności:

* Zainstaluj hello [aplikacji RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Ta aplikacja jest zintegrowany z pakietu Office aplikacji przez zainstalowanie pakietu Office dodatek tak, aby użytkownikom ochronę plików bezpośrednio.
* Skonfiguruj aplikacje i toosupport usług Azure RMS
* Utwórz [szablonów niestandardowych](https://technet.microsoft.com/library/dn642472.aspx) która odzwierciedla wymagania firmy. Na przykład: szablon do górnej poufne dane, które powinny być stosowane w wszystkich ściśle tajne związane z wiadomości e-mail.

Organizacje, które są słabe na [klasyfikacji danych](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) i ochrona plików może być bardziej narażony wycieku toodata. Bez ochrony prawidłowego pliku organizacji nie będą mogli tooobtain informacje biznesowe, monitorowanie nadużyć należy również uniemożliwić toofiles nieautoryzowanym dostępem.

Dodatkowe informacje na temat usługi Azure RMS od przeczytania artykułu hello [wprowadzenie do korzystania z usługi Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).
