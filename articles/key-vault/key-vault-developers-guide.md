---
title: Przewodnik dewelopera aaaAzure klucza magazynu
description: "Deweloperzy mogą używać usługi Azure Key Vault toomanage kluczy kryptograficznych w środowisku Microsoft Azure hello."
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 631cea1315964cd0b97e8b2cf3311754230fb801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-developers-guide"></a>Przewodnik dewelopera usługi Azure Key Vault

Magazyn kluczy umożliwia toosecurely dostęp do poufnych informacji w aplikacjach:

- Klucze i klucze tajne, które są chronione bez konieczności toowrite hello kod samodzielnie i są toouse łatwo można je z aplikacjami.
- Są możliwe toohave własnych klientów i zarządzanie własne klucze, więc użytkownik może skupić się na dostarczaniu hello podstawowych funkcji oprogramowania. W ten sposób aplikacje nie będą właścicielami odpowiedzialności hello ani zobowiązań potencjalnych klientów dzierżawy kluczy i kluczy tajnych.
- Aplikacja może używać klucze do podpisywania i szyfrowania jeszcze utrzymują zarządzania kluczami hello zewnętrznych z aplikacji, umożliwiając toobe Twojego rozwiązania odpowiedniego jako aplikację geograficznie rozproszonych.
- Począwszy od wersji hello września 2016 r. Klucz magazynu, aplikacje można teraz używać usługi Key Vault [certyfikaty](https://docs.microsoft.com/rest/api/keyvault/certificate-operations). Aby uzyskać więcej informacji, zobacz [o kluczy, kluczy tajnych i certyfikaty](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).

Aby uzyskać więcej ogólnych informacji dotyczących usługi Azure Key Vault, zobacz [co to jest magazyn kluczy](key-vault-whatis.md).

## <a name="public-previews"></a>Podglądy publiczny

Okresowo wydania publicznej wersji zapoznawczej nowych funkcji usługi Key Vault. Spróbuj się one i Daj nam znać, co myślisz za pośrednictwem azurekeyvault@microsoft.com, adres e-mail naszych opinii.

### <a name="storage-account-keys---july-10-2017"></a>Klucze konta magazynu - 10 lipca 2017 r.

>[!NOTE]
>Dla tej aktualizacji usługi Azure Key Vault tylko hello **klucze konta magazynu** jest funkcja w wersji zapoznawczej.

Ta wersja zapoznawcza zawiera naszej nowej klucze konta magazynu funkcji dostępnych za pośrednictwem tych interfejsów; [.NET / C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) i [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/). 

Aby uzyskać więcej informacji na powitania nowa funkcja klucze konta magazynu, zobacz [omówienie klucze konta magazynu usługi Azure Key Vault](key-vault-ovw-storage-keys.md).

## <a name="videos"></a>Filmy wideo

To wideo pokazuje, jak toocreate własnego klucza magazynu i jak toouse z hello Hello Key Vault przykładowej aplikacji.

- [Magazyn kluczy developer — Przewodnik Szybki start](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

Zasoby w powyższym wideo:

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Usługi Azure Key Vault przykładowy kod](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>Tworzenie i zarządzanie nimi magazynów kluczy

Przed rozpoczęciem pracy z usługą Azure Key Vault w kodzie, możesz utworzyć i Zarządzanie magazynami za pośrednictwem REST, szablony usługi Resource Manager, programu PowerShell lub interfejsu wiersza polecenia, zgodnie z opisem w hello następujące artykuły:

- [Tworzenie i zarządzanie nimi magazynów kluczy z REST](https://docs.microsoft.com/rest/api/keyvault/)
- [Tworzenie i zarządzanie nimi magazynów kluczy przy użyciu programu PowerShell](key-vault-get-started.md)
- [Tworzenie i zarządzanie nimi magazynów kluczy za pomocą interfejsu wiersza polecenia](key-vault-manage-with-cli2.md)
- [Utwórz magazyn kluczy i Dodaj klucz tajny za pomocą szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Operacje magazynów kluczy uwierzytelniania za pomocą usługi AAD i autoryzacji za pomocą zasad dostępu do magazynu kluczy własnych, zdefiniowanych na magazynie.

## <a name="coding-with-key-vault"></a>Kodowanie z magazynu kluczy

Hello system zarządzania Key Vault dla programistów składa się z kilku interfejsów o REST jako hello foundation. Za pośrednictwem interfejsu REST hello wszystkie zasoby magazynów kluczy są dostępne; klucze kluczy tajnych i certyfikatów. [Dokumentacja interfejsu API REST magazynu kluczy](https://docs.microsoft.com/rest/api/keyvault/). 

### <a name="supported-programming-languages"></a>Obsługiwane języki programowania

#### <a name="net"></a>.NET

- [Interfejs API .NET porządkowy dla usługi Key Vault](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

Aby uzyskać więcej informacji na powitania wersji 2.x hello zestawu .NET SDK, zobacz hello [informacje o wersji](key-vault-dotnet2api-release-notes.md).

#### <a name="java"></a>Java

- [Java SDK dla magazynu kluczy](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

W środowisku Node.js interfejs API zarządzania magazynem hello i interfejsu API obiektu magazynu hello są niezależne. Zarządzanie magazynem klucza umożliwia tworzenie i aktualizowanie klucza magazynu. Interfejs API operacji magazynu kluczy jest do pracy z magazynem obiektów, na przykład; klucze kluczy tajnych i certyfikatów. 

- [Dokumentacja interfejsu API środowiska node.js dla klucza zarządzania magazynem](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Dokumentacja interfejsu API środowiska node.js dla operacji magazynu kluczy](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>Szybki start

- [Utwórz magazyn kluczy](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Wprowadzenie do korzystania z usługi Key Vault w środowisku Node.js](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>Przykłady kodu

Przykłady pełną za pomocą usługi Key Vault z aplikacji można znaleźć:

- [Przykłady kodu w usłudze Azure Key Vault](http://www.microsoft.com/download/details.aspx?id=45343) -.NET przykładowej aplikacji *HelloKeyVault* i przykład usługi sieci web platformy Azure. 
- [Użyj usługi Azure Key Vault z aplikacji sieci Web](key-vault-use-from-web-application.md) -toohelp samouczka, dowiesz się, jak toouse Azure klucza magazynu z aplikacji sieci web na platformie Azure. 

## <a name="how-tos"></a>Poradniki

Witaj następujące artykuły i scenariusze zawierają specyficzne dla zadania wskazówki dotyczące pracy z usługą Azure Key Vault:

- [Przenieś zmiany Identyfikatora dzierżawcy magazynu kluczy po subskrypcji](key-vault-subscription-move-fix.md) — po przeniesieniu subskrypcji platformy Azure z dzierżawy tootenant B, Twoje istniejące magazynów kluczy są niedostępne podmiotów hello zabezpieczeń (Użytkownicy i aplikacje) w dzierżawie poprawka B. używania tego przewodnika.
- [Uzyskiwanie dostępu do usługi Key Vault za zaporą](key-vault-access-behind-firewall.md) -tooaccess klucza magazynu z magazynu kluczy klienta aplikacji potrzeb toobe stanie tooaccess wielu punkty końcowe dla różnych funkcji.
- [Jak tooGenerate i klucze Transfer HSM-Protected dla usługi Azure Key Vault](key-vault-hsm-protected-keys.md) — dzięki temu można zaplanować, generowanie i następnie przenieść toouse własne klucze chronione przez moduł HSM z usługi Azure Key Vault.
- [Jak zabezpieczyć toopass wartości (na przykład hasła) podczas wdrażania](../azure-resource-manager/resource-manager-keyvault-parameter.md) — gdy będziesz potrzebować toopass bezpiecznego wartość (na przykład hasło) jako parametr podczas wdrażania, można przechowywać tej wartości jako klucza tajnego w wartości hello odwołanie do usługi Azure Key Vault i w innych Szablony Menedżera zasobów.
- [Jak toouse Key Vault rozszerzonego zarządzania kluczami z programem SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) — Witaj Łącznik usług SQL Server dla usługi Azure Key Vault umożliwia programu SQL Server i SQL w wirtualna tooleverage hello Azure Key Vault usługi jako dostawcy rozszerzonego zarządzania klucza (EKM) tooprotect jego szyfrowania kluczy dla łącza aplikacji; Przezroczystego szyfrowania danych, szyfrowania kopii zapasowych i szyfrowanie na poziomie kolumny.
- [Jak toodeploy tooVMs certyfikaty z magazynu kluczy](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) — aplikacji w chmurze uruchomione na maszynie wirtualnej na potrzeby Azure certyfikatu. Jak uzyskać ten certyfikat do tej maszyny Wirtualnej dzisiaj?
- [Jak tooset się Key Vault z tooend zakończenia klucza obracanie i inspekcji](key-vault-key-rotation-log-monitoring.md) — to przedstawiono sposób tooset rotacją kluczy i inspekcji w usłudze Azure Key Vault.
- [Wdrażanie certyfikatów aplikacji sieci Web Azure za pomocą usługi Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) zawiera instrukcje krok po kroku dotyczące wdrażania certyfikaty przechowywane w magazynie kluczy jako część [certyfikatu usługi aplikacji](https://azure.microsoft.com/blog/internals-of-app-service-certificate/) oferty.
- [Przyznaj uprawnienie toomany aplikacji tooaccess magazynu kluczy](key-vault-group-permissions-for-apps.md) zasady kontroli dostępu do magazynu kluczy obsługuje tylko wpisy 16. Można jednak utworzyć grupy zabezpieczeń usługi Azure Active Directory. Dodaj wszystkie hello skojarzona grupa zabezpieczeń toothis podmiotów zabezpieczeń usługi, a następnie przyznać dostęp toothis zabezpieczeń grupy tooKey magazynu.
- Dla poszczególnych zadań więcej pomocy na temat integracji i przy użyciu magazynów kluczy w usłudze Azure, zobacz [przykłady szablonów usługi Azure Resource Manager Nowak Ryan dla usługi Key Vault](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
- [Jak toouse Key Vault soft usunięcie z interfejsu wiersza polecenia](key-vault-soft-delete-cli.md) prowadzi użytkownika przez użycie hello i cyklem życia magazyn kluczy i różnych obiektów magazynu kluczy z usuwania nietrwałego, włączone.
- [Jak toouse Key Vault soft usunięcie przy użyciu programu PowerShell](key-vault-soft-delete-powershell.md) prowadzi użytkownika przez użycie hello i cyklem życia magazyn kluczy i różnych obiektów magazynu kluczy z usuwania nietrwałego, włączone.

## <a name="integrated-with-key-vault"></a>Zintegrowana z magazynu kluczy

Artykuły te są o innych scenariuszy i użyj lub zintegrować z magazynu kluczy usług.

- [Szyfrowanie dysków Azure](../security/azure-security-disk-encryption.md) wykorzystanie hello branżowymi [funkcji BitLocker](https://technet.microsoft.com/library/cc732774.aspx) funkcji systemu Windows i hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) funkcji szyfrowania woluminów tooprovide Linux hello systemu operacyjnego i danych hello dyski. rozwiązanie Hello jest zintegrowany z usługi Azure Key Vault toohelp sterowania i zarządzania hello dysku szyfrowania kluczy i kluczy tajnych w magazynie kluczy subskrypcji, przy jednoczesnym zapewnieniu, że wszystkie dane w hello dysków maszyny wirtualnej są szyfrowane, gdy w magazynie Azure.
- [Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) udostępniana opcja szyfrowania danych, które są przechowywane na koncie hello. Zarządzania kluczami Data Lake Store zapewnia dwa tryby zarządzania kluczy szyfrowania głównego (MEKs), które są wymagane do odszyfrowywania danych przechowywanych w hello usługi Data Lake Store. Można albo programowi Data Lake Store Zarządzanie hello MEKs, lub wybierz własność tooretain MEKs hello przy użyciu konta usługi Azure Key Vault. Tryb hello zarządzania kluczami należy określić podczas tworzenia konta usługi Data Lake Store. 
- [Usługa Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) pozwala toomanager klucza dzierżawy. Na przykład firma Microsoft zarządza kluczem dzierżawy (hello ustawienie domyślne), można zarządzać własną toocomply klucza dzierżawy z konkretnymi przepisami mającymi zastosowanie tooyour organizacji. Zarządzanie własnym kluczem dzierżawy jest również, tooas określonego Przynieś własny klucz lub BYOK.

## <a name="key-vault-overviews-and-concepts"></a>Omówienie magazynu kluczy i pojęć

- [Zachowanie usuwania nietrwałego Key Vault](key-vault-ovw-soft-delete.md) opisuje funkcja, która umożliwia odzyskiwanie usuniętych obiektów, czy usunięcie hello było przypadkowym lub zamierzone.
- [Ograniczanie klienta usługi Key Vault](key-vault-ovw-throttling.md) kieruje użytkowników podstawowych pojęć toohello ograniczania przepustowości i oferuje podejście do aplikacji.
- [Omówienie klucze konta magazynu usługi Key Vault](key-vault-ovw-storage-keys.md) opisano klucze konta magazynu Azure integracji magazynu kluczy hello.
- [Środowiska security World usługi Key Vault](key-vault-ovw-security-worlds.md) opisuje hello relacje między regionami i obszary zabezpieczeń.

## <a name="social"></a>Społeczności

- [Blog magazyn kluczy](http://aka.ms/kvblog)
- [Forum magazyn kluczy](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>Obsługa biblioteki

- [Biblioteka podstawowa magazynu Microsoft Azure klucza](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) zapewnia **IKey** i **IKeyResolver** interfejsy do lokalizowania kluczy z identyfikatorów i wykonywanie operacji z kluczami.
- [Rozszerzeń platformy Microsoft Azure Key Vault](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) zapewnia rozszerzone możliwości usługi Azure Key Vault.


