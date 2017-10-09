---
title: "Funkcje aaaSecurity, które mogą być używane z usługą Azure Storage | Dokumentacja firmy Microsoft"
description: " Ten artykuł zawiera omówienie funkcji zabezpieczeń platformy Azure core hello, których można użyć z usługą Azure Storage. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 521180dc-2cc9-43f1-ae87-2701de7ca6b8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 663cd2705527957d21ff9475a6322b42a16c95e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-overview"></a>Omówienie zabezpieczeń usługi Azure storage
Magazyn Azure to rozwiązanie magazynu hello w chmurze dla nowoczesnych aplikacji, które polegają na trwałości, dostępności i skalowalności toomeet hello potrzeb klientów. Magazyn Azure oferuje rozbudowany zestaw funkcji zabezpieczeń:

* Konto magazynu Hello mogą być chronione przy użyciu kontroli dostępu opartej na rolach i Azure Active Directory.
* Dane mogą być chronione przesyłanych między aplikacją a Azure za pomocą szyfrowania po stronie klienta, HTTPS lub SMB 3.0.
* Dane można ustawić toobe automatycznie szyfrowane podczas zapisywane tooAzure magazynu przy użyciu szyfrowania usługi magazynu.
* Systemu operacyjnego i dysków z danymi używanych przez maszyny wirtualne można ustawić toobe zaszyfrowane za pomocą szyfrowania dysków Azure.
* Obiekty danych toohello delegowanego dostępu w usłudze Azure Storage można otrzymać za pomocą sygnatury dostępu współdzielonego.
* Hello metoda uwierzytelniania używana przez inną przy uzyskiwaniu dostępu do magazynu mogą być śledzone za pomocą analityka magazynu.

Aby uzyskać bardziej szczegółowy widok zabezpieczeń w usłudze Azure Storage, zobacz hello [przewodnik zabezpieczeń usługi Azure Storage](../storage/common/storage-security-guide.md). Ten przewodnik zawiera nowości w funkcji zabezpieczeń hello magazynu Azure, takie jak klucze konta magazynu, szyfrowanie danych przesyłanych i rest i analiza magazynu.

Ten artykuł zawiera omówienie funkcji zabezpieczeń platformy Azure, których można użyć z usługą Azure Storage. Łącza podano tooarticles, który podać szczegóły dotyczące każdej funkcji, aby dowiedzieć się więcej.

Poniżej przedstawiono toobe funkcje podstawowe hello omówione w tym artykule:

* Kontrola dostępu oparta na rolach
* Obiekty toostorage dostęp delegowany
* Szyfrowanie podczas przesyłania
* Szyfrowanie Szyfrowanie usługi rest i magazynowania
* Usługa Azure Disk Encryption
* W usłudze Azure Key Vault

## <a name="role-based-access-control-rbac"></a>Kontrola dostępu oparta na rolach (RBAC)
Można zabezpieczyć konto magazynu z kontroli dostępu opartej na rolach (RBAC). Ograniczanie dostępu oparte na powitania [muszą tooknow](https://en.wikipedia.org/wiki/Need_to_know) i [najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege) jest zasad bezpieczeństwa dla firm, które chcą tooenforce zasad zabezpieczeń dla dostępu do danych. Te prawa dostępu są udzielane przez przypisywanie hello odpowiednie RBAC roli toogroups i aplikacje w określonego zakresu. Można użyć [wbudowane role RBAC](../active-directory/role-based-access-built-in-roles.md), takich jak współautora konta magazynu, tooassign uprawnienia toousers.

Więcej informacji:

* [Kontrola dostępu oparta na rolach w usłudze Azure Active Directory](../active-directory/role-based-access-control-configure.md)

## <a name="delegated-access-toostorage-objects"></a>Obiekty toostorage dostęp delegowany
Sygnatury dostępu współdzielonego (SAS) zapewnia dostęp delegowany tooresources na koncie magazynu. Witaj SAS oznacza, że można udzielać się, że klient ograniczone uprawnienia tooobjects na koncie magazynu w określonym przedziale czasu i z określonym zestawem uprawnień. Ograniczone uprawnienia można przyznać bez konieczności tooshare klucze dostępu do Twojego konta. Witaj SAS jest identyfikatorem URI, który obejmuje w jego parametrów zapytania, wszystkie informacje hello niezbędne dla zasobu magazynu tooa dostępu uwierzytelnionego. tooaccess zasoby pamięci masowej z hello SAS powitania klienta musi tylko tooprovide hello SAS toohello odpowiedniego konstruktora lub metody.

Więcej informacji:

* [Opis hello SAS modelu](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [Tworzenie i używanie sygnatury dostępu Współdzielonego z magazynem obiektów Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md)

## <a name="encryption-in-transit"></a>Szyfrowanie podczas przesyłania
Szyfrowanie podczas przesyłania jest mechanizm ochrony danych podczas ich przesyłania w sieciach. Z usługą Azure Storage, można zabezpieczyć dane przy użyciu:

* [Szyfrowanie na poziomie transportu](../storage/common/storage-security-guide.md#encryption-in-transit), taki jak HTTPS podczas transferu danych do i z usługi Azure Storage.
* [Połączenie szyfrowania](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), takimi jak szyfrowanie protokołu SMB 3.0 udziałów plików Azure.
* [Szyfrowanie po stronie klienta](../storage/common/storage-security-guide.md#using-client-side-encryption-to-secure-data-that-you-send-to-storage), tooencrypt hello danych, zanim zostanie przekazany do magazynu i toodecrypt danych powitania po przeniesieniu poza magazynu.

Dowiedz się więcej na temat szyfrowania po stronie klienta:

* [Szyfrowanie po stronie klienta dla usługi Microsoft Azure Storage](https://blogs.msdn.microsoft.com/windowsazurestorage/2015/04/28/client-side-encryption-for-microsoft-azure-storage-preview/)
* [Zabezpieczenia chmury sterują serii: szyfrowanie przesyłanych danych](http://blogs.microsoft.com/cybertrust/2015/08/10/cloud-security-controls-series-encrypting-data-in-transit/)

## <a name="encryption-at-rest"></a>Szyfrowanie w spoczynku
W przypadku wielu organizacji [szyfrowanie danych magazynowanych](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) jest obowiązkowy krok na drodze danych suwerenności prywatności, zgodności i danych. Istnieją trzy funkcje platformy Azure, które zapewniają szyfrowania danych, która jest "w stanie spoczynku":

* [Szyfrowanie usługi Magazyn](../storage/common/storage-security-guide.md#encryption-at-rest) pozwala toorequest, że Usługa magazynu hello automatycznie szyfrowania danych podczas jej pisania tooAzure magazynu.
* [Szyfrowanie po stronie klienta](../storage/common/storage-security-guide.md#client-side-encryption) oferuje także funkcję hello szyfrowania w stanie spoczynku.
* [Szyfrowanie dysków Azure](../storage/common/storage-security-guide.md#using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) tooencrypt dysków hello systemu operacyjnego i dysków danych używanych przez maszyny wirtualne IaaS.

Dowiedz się więcej na temat szyfrowanie usługi magazynu:

* [Szyfrowanie usługi Magazyn Azure](https://azure.microsoft.com/services/storage/) jest dostępna dla [magazyn obiektów Blob Azure](https://azure.microsoft.com/services/storage/blobs/). Aby uzyskać szczegółowe informacje dotyczące innych typów magazynu Azure, zobacz [pliku](https://azure.microsoft.com/services/storage/files/), [dysku (magazyn w warstwie Premium)](https://azure.microsoft.com/services/storage/premium-storage/), [tabeli](https://azure.microsoft.com/services/storage/tables/), i [kolejki](https://azure.microsoft.com/services/storage/queues/).
* [Szyfrowanie usługi Magazyn Azure dla przechowywanych danych](../storage/common/storage-service-encryption.md)

## <a name="azure-disk-encryption"></a>Usługa Azure Disk Encryption
Azure szyfrowania dysków na maszynach wirtualnych (VM) ułatwia adres zabezpieczeń organizacji i wymagania zgodności przez szyfrowanie dysków maszyny Wirtualnej (w tym rozruchu i dysków z danymi) przy użyciu kluczy i zasad kontroli w [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

Szyfrowanie dysków dla maszyn wirtualnych działa w przypadku systemów operacyjnych Linux i Windows. Używa usługi Key Vault toohelp zabezpieczenia, zarządzanie i inspekcja użycia kluczy szyfrowania dysku. Wszystkie dane hello dysków maszyny Wirtualnej jest szyfrowane, gdy przy użyciu technologii szyfrowania standardowych kont usługi Azure Storage. Szyfrowanie dysków rozwiązania dla systemu Windows Hello jest oparta na [szyfrowania dysków funkcją BitLocker Microsoft](https://technet.microsoft.com/library/cc732774.aspx), i hello Linux rozwiązanie opiera się na [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt).

Więcej informacji:

* [Szyfrowanie dysków Azure dla systemu Windows i maszyn wirtualnych systemu Linux IaaS](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)

## <a name="azure-key-vault"></a>W usłudze Azure Key Vault
Używa szyfrowania dysków Azure [usługi Azure Key Vault](https://azure.microsoft.com/services/key-vault/) toohelp podczas sterowania i zarządzania nimi klucze szyfrowania dysku i kluczy tajnych w ramach subskrypcji magazynu kluczy, zapewniając, że wszystkie dane w hello dysków maszyny wirtualnej są szyfrowane, gdy w platformy Azure Magazyn. Należy używać kluczy tooaudit magazyn kluczy i użycia zasad.

Więcej informacji:

* [Co to jest usługa Azure Key Vault?](../key-vault/key-vault-whatis.md)
* [Wprowadzenie do usługi Azure Key Vault](../key-vault/key-vault-get-started.md)
