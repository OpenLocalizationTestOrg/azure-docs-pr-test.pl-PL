---
title: "aaaSecuring PaaS aplikacji przy użyciu usługi Azure Storage | Dokumentacja firmy Microsoft"
description: " Więcej informacji na temat zabezpieczeń usługi Azure Storage najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: TomShinder
ms.openlocfilehash: 3fed75cb121e7f32eb8b948ee12ca35fb25eca7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-storage"></a>Zabezpieczanie PaaS w sieci web i aplikacji dla urządzeń przenośnych przy użyciu usługi Azure Storage
W tym artykule omówiono kolekcję usługi Azure Storage zabezpieczeń najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. Następujące najlepsze rozwiązania są uzyskiwane z wiemy z doświadczenia z platformy Azure i doświadczenia hello klientów, takich jak samodzielnie.

Witaj [przewodnik zabezpieczeń usługi Azure Storage](../storage/common/storage-security-guide.md) jest doskonałym źródłem szczegółowe informacje dotyczące usługi Azure Storage i zabezpieczeń.  W tym artykule opisano na wysokim poziomie niektóre pojęcia hello znaleźć w przewodniku po zabezpieczeniach hello i przewodnik po zabezpieczeniach toohello łącza, a także innych źródeł, aby uzyskać więcej informacji.

## <a name="azure-storage"></a>Azure Storage
Azure ułatwia możliwe toodeploy i Użyj magazynu w sposób nieosiągalne łatwo lokalnymi. Z usługą Azure storage można osiągnąć wysoką skalowalność i dostępność o stosunkowo dużego wysiłku. Nie tylko słowo foundation hello magazynu Azure dla systemu Windows i maszyn wirtualnych systemu Linux platformy Azure, może również obsługiwać dużych aplikacji rozproszonej.

Usługa Azure storage udostępnia następujące cztery usługi hello: obiektu Blob magazynu, Magazyn tabel, magazyn kolejek i magazyn plików. toolearn więcej, zobacz [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/storage-introduction.md).

## <a name="best-practices"></a>Najlepsze praktyki
W tym artykule opisano hello następujące najlepsze rozwiązania:

- Ochrona dostępu do:
   - Sygnatury dostępu współdzielonego (SAS)
   - Dysk zarządzany
   - Kontrola dostępu oparta na rolach (RBAC)

- Szyfrowanie magazynu:
   - Szyfrowanie po stronie klienta dla danych wysokiej wartości.
   - Szyfrowanie dysków Azure maszynach wirtualnych (VM)
   - Szyfrowanie usługi Storage

## <a name="access-protection"></a>Ochrona dostępu do
### <a name="use-shared-access-signature-instead-of-a-storage-account-key"></a>Użyj sygnatura dostępu współdzielonego zamiast klucz konta magazynu

W rozwiązaniu IaaS, zazwyczaj uruchomionych maszyn wirtualnych systemu Windows Server lub Linux pliki są chronione przed ujawnieniem oraz manipulacją zagrożeń przy użyciu mechanizmy kontroli dostępu. W systemie Windows można użyć [(ACL). listy kontroli dostępu](../virtual-network/virtual-networks-acl.md) i w systemie Linux prawdopodobnie użyje [chmod](https://en.wikipedia.org/wiki/Chmod). Zasadniczo jest dokładnie co może zrobić, jeśli zostały ochrona plików na serwerze w centrum danych dzisiaj.

PaaS różni się. Jeden z hello najbardziej typowe sposoby toostore plików w systemie Microsoft Azure jest toouse [magazynu obiektów Blob Azure](../storage/storage-dotnet-how-to-use-blobs.md). Różnica między magazynu obiektów Blob i innych magazyn plików jest hello plik we/wy i metody ochrony hello z We/Wy plików.

Bardzo ważne jest kontrola dostępu. toohelp kontrolować dostęp do magazynu tooAzure, hello system będzie generował dwa klucze konta magazynu 512-bitowe (SAKs) gdy użytkownik [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md). Witaj poziomu nadmiarowości klucza umożliwia możesz tooavoid usługi przerwania podczas rutynowej rotacją kluczy.

Tylko należy dostępny toothose odpowiedzialny za kontroli dostępu do magazynu kluczy dostępu do magazynu i są klucze tajne o wysokim priorytecie. Jeśli hello nieodpowiednie osoby uzyskanie dostępu do kluczy toothese, ich będzie mają pełną kontrolę nad magazynu i można zastąpić, usuń lub Dodaj toostorage plików. W tym złośliwym oprogramowaniem i innych typów zawartości, które potencjalnie może naruszyć organizacji lub dla klientów.

Nadal potrzebujesz tooobjects dostępu tooprovide sposób, w magazynie. tooprovide bardziej szczegółowego dostępu, możesz skorzystać z [sygnatura dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). Hello SAS umożliwia dla Ciebie tooshare określonych obiektów w magazynie dla wstępnie zdefiniowanego interwału czasu i z określonymi uprawnieniami. Sygnaturę dostępu współdzielonego umożliwia toodefine:

- Interwał powitania za pośrednictwem których hello jest prawidłowa, w tym hello czas rozpoczęcia i czas wygaśnięcia hello sygnatury dostępu Współdzielonego.
- Witaj uprawnienia przyznane przez hello sygnatury dostępu Współdzielonego. Na przykład sygnatury dostępu Współdzielonego w obiekcie blob może udzielić odczytu użytkownika i obiektów blob toothat uprawnienia do zapisu, ale nie usunąć uprawnienia.
- Opcjonalne adres IP lub zakres adresów IP, z których akceptuje usługi Azure Storage hello sygnatury dostępu Współdzielonego. Na przykład może określić zakres adresów IP należących do organizacji tooyour. Zapewnia to innej miary zabezpieczeń dla sieci SAS.
- Protokół Hello służącym usługi Azure Storage akceptuje hello sygnatury dostępu Współdzielonego. Możesz użyć tego tooclients opcjonalny parametr toorestrict dostępu przy użyciu protokołu HTTPS.

Sygnatury dostępu Współdzielonego umożliwia tooshare zawartości hello sposób tooshare jego pracy bez podania kluczy konta magazynu. Zawsze przy użyciu sygnatury dostępu Współdzielonego w aplikacji jest tooshare bezpieczny sposób zasobów magazynu bez naruszania kluczy konta magazynu.

toolearn więcej, zobacz [przy użyciu sygnatury dostępu współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS). więcej informacji na temat potencjalnego zagrożenia i zalecenia toomitigate toolearn te zagrożenia, zobacz [najlepszych rozwiązań przy użyciu sygnatury dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="use-managed-disks-for-vms"></a>Użyj zarządzanego dyski dla maszyn wirtualnych

Po wybraniu [dysków zarządzanych Azure](../storage/storage-managed-disks-overview.md), Azure zarządza kontami magazynu hello, których używasz dla dysków maszyny Wirtualnej. Toodo wystarczy wybrać typ hello dysku (Premium lub Standard) oraz rozmiar dysku hello; Magazyn Azure będzie wykonywać hello rest. Nie masz tooworry dotyczących ograniczeń skalowalności, które mogą mieć w przeciwnym razie wymagane konta magazynu toomultiple tooyou.

toolearn więcej, zobacz [— często zadawane pytania o zarządzanych i niezarządzanych dyski premium](../storage/storage-faq-for-disks.md).

### <a name="use-role-based-access-control"></a>Za pomocą kontroli dostępu opartej na rolach

Wcześniej wspomniano, bez narażania klucz konta magazynu konta przy użyciu tooobjects dostępu toogrant ograniczony dostęp do sygnatury dostępu Współdzielonego w klientach tooother konta magazynu. Czasami hello ryzyko związane z określoną operację względem konta magazynu przeważają korzyści hello SAS. Czasami jest prostsze dostępu toomanage w inny sposób.

Inny sposób toomanage dostępu jest toouse [kontroli dostępu](../active-directory/role-based-access-control-what-is.md) (RBAC). Z RBAC, skupić się na zapewniając pracownikom hello dokładne uprawnienia, które są im potrzebne, na podstawie tooknow potrzeby hello i co najmniej uprawnień zabezpieczeń zasad. Za dużo uprawnienia mogą uwidaczniać tooattackers konta. Za mało uprawnienia oznacza, że pracownicy nie można pobrać ich pracować wydajnie. RBAC pomaga rozwiązać ten problem, oferując precyzyjne zarządzanie dostępem dla platformy Azure. Jest to konieczne w przypadku organizacji, które mają tooenforce zasad zabezpieczeń dla dostępu do danych.

Można wykorzystać wbudowane role RBAC w toousers uprawnienia tooassign platformy Azure. Należy rozważyć użycie współautora konta magazynu dla operatorów chmury, które wymagają konta magazynu toomanage i klasycznego współautora konta magazynu roli toomanage klasycznych kont magazynu. Dla operatorów chmury wymagające toomanage maszyn wirtualnych, ale nie hello sieci wirtualnej lub toowhich konta magazynu, które są połączone należy rozważyć dodanie ich toohello roli współautora maszyny wirtualnej.

Organizacje, które nie wymusić kontrolę dostępu danych dzięki wykorzystaniu możliwości, takie jak RBAC może nadanie więcej uprawnień niż jest to niezbędne dla użytkowników. Może to spowodować naruszenie toodata zezwalając toodata dostępu do niektórych użytkowników, które nie powinny mieć hello pierwsze miejsce.

toolearn znaleźć więcej informacji na temat RBAC:

- [Kontrola dostępu oparta na rolach na platformie Azure](../active-directory/role-based-access-control-configure.md)
- [Wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md)
- [Przewodnik po zabezpieczeniach magazynu Azure](../storage/common/storage-security-guide.md) do szczegółów w sposób toosecure, konto magazynu, z RBAC

## <a name="storage-encryption"></a>Szyfrowanie magazynu
### <a name="use-client-side-encryption-for-high-value-data"></a>Użyj szyfrowania po stronie klienta danych wysokiej wartości.

Umożliwia szyfrowanie po stronie klienta, możesz tooprogrammatically szyfrowanie przesyłanych danych przed przekazaniem tooAzure magazynu i programowo odszyfrowywania danych podczas pobierania go z magazynu.  Zapewnia szyfrowanie danych podczas przesyłania, ale również zapewnia szyfrowanie danych magazynowanych.  Szyfrowanie po stronie klienta jest hello najbezpieczniejszą metodą szyfrowania danych, ale wymagają toomake programowe zmiany tooyour aplikacji i wprowadzone procesy zarządzania kluczami.

Szyfrowanie po stronie klienta umożliwia również toohave wyłączną kontrolę nad kluczami szyfrowania.  Można wygenerować i zarządzanie kluczami szyfrowania.  Szyfrowanie po stronie klienta używa technikę koperty, gdzie hello biblioteki klienta magazynu Azure generuje zawartości klucza szyfrowania (CEK), który jest następnie opakowane (zaszyfrowane) przy użyciu hello klucza szyfrowania klucza (KEK). Hello KEK jest identyfikowany przez identyfikator klucza i można parę klucza asymetrycznego lub klucza symetrycznego i może być zarządzany lokalnie lub przechowywane w [usługi Azure Key Vault](../key-vault/key-vault-whatis.md).

Szyfrowanie po stronie klienta jest wbudowana w hello Java i biblioteki klienta magazynu .NET hello.  Zobacz [szyfrowania po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](../storage/storage-client-side-encryption.md) informacji na temat szyfrowania danych w aplikacjach klienckich i generowania i zarządzanie kluczy szyfrowania.

### <a name="azure-disk-encryption-for-vms"></a>Szyfrowanie dysków Azure dla maszyn wirtualnych
Szyfrowanie dysków Azure jest możliwość, która pomaga szyfrowania dysków maszyny wirtualnej systemu Windows i Linux IaaS. Szyfrowanie dysków Azure wykorzystuje hello branżowy standard funkcji BitLocker funkcji systemu Windows i DM-Crypt hello funkcji szyfrowania woluminów tooprovide Linux hello systemu operacyjnego i dysków danych hello. rozwiązanie Hello jest zintegrowany z usługi Azure Key Vault toohelp sterowania i zarządzania hello szyfrowanie dysków kluczy i kluczy tajnych w magazynie kluczy subskrypcji. rozwiązanie Hello gwarantuje również, że wszystkie dane na powitania dysków maszyny wirtualnej są szyfrowane, gdy w magazynie Azure.

Zobacz [szyfrowania dysków Azure dla systemu Windows oraz maszyny wirtualne systemu Linux IaaS](azure-security-disk-encryption.md).

### <a name="storage-service-encryption"></a>Szyfrowanie usługi Storage
Gdy [szyfrowanie usługi Magazyn](../storage/storage-service-encryption.md) magazyn plików jest włączona, hello dane są szyfrowane automatycznie przy użyciu szyfrowania AES 256. Firma Microsoft podchodzi do hello szyfrowania, odszyfrowywania i zarządzania kluczami. Ta funkcja jest dostępna dla typów nadmiarowość LRS i GRS.

## <a name="next-steps"></a>Następne kroki
W tym artykule wprowadzono tooa kolekcji usługi Azure Storage zabezpieczeń najlepsze rozwiązania dotyczące zabezpieczania PaaS w sieci web i aplikacji dla urządzeń przenośnych. toolearn więcej informacji na temat zabezpieczania wdrożeń typu PaaS, zobacz:

- [Zabezpieczanie wdrożeń typu PaaS](security-paas-deployments.md)
- [Zabezpieczanie PaaS w sieci web i aplikacji dla urządzeń przenośnych za pomocą usługi aplikacji Azure](security-paas-applications-using-app-services.md)
- [Zabezpieczanie PaaS baz danych na platformie Azure](security-paas-applications-using-sql.md)
