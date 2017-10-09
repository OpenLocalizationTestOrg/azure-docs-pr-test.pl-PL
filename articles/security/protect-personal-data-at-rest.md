---
title: Ochrona danych osobowych magazynowane z szyfrowaniem aaaAzure | Dokumentacja firmy Microsoft
description: "W tym artykule jest częścią serii, pomaga użyć danych osobowych Azure tooprotect"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>Technologii szyfrowania Azure: ochrony danych osobowych w stanie spoczynku z szyfrowaniem

Ten artykuł pomaga w zrozumieniu i użytkowaniu danych toosecure technologii szyfrowania Azure w stanie spoczynku.

Szyfrowanie danych magazynowanych jest jako najlepsze rozwiązanie tooprotect poufnych i osobistych danych i toomeet zgodności i wymaganiami dotyczącymi ochrony prywatności danych.
Szyfrowanie rest jest zaprojektowana tooprevent atakująca hello uzyskanie dostępu do danych hello bez szyfrowania, zapewniając hello, którego dane są szyfrowane, gdy na dysku.

## <a name="scenario"></a>Scenariusz 

Firma rejs dużych, siedzibą hello Stanów Zjednoczonych, rozwija trasy toooffer jego operacji w hello Śródziemnego i Bałtyckiego mórz oraz hello brytyjskich. toosupport tych działań uzyskała mniejszych rejs wiersze na podstawie we Włoszech, Niemczech, Dania i hello Zjednoczone Królestwo

Witaj firma korzysta z danych firmowych toostore Microsoft Azure w chmurze hello. Może to obejmować pracowników i/lub klienta informacje takie jak:

- adresy
- Numery telefonów
- Numery identyfikacyjne podatku
- Inne informacje
- informacje o karcie kredytowej

Hello firmy muszą chronić prywatność hello pracowników i klientów danych podczas przesyłania danych dostępny toothose działów, które go potrzebują. (na przykład lista płac i zastrzeżenia działów)

wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność zawierający dane osobowe tootrack relacje z bieżących i starszych klientów.

### <a name="problem-statement"></a>Opis problemu

Hello firmy muszą chronić prywatność hello pracowników i klientów danych osobowych podczas wprowadzania danych dostępny toothose działów, które go potrzebują (na przykład lista płac i zastrzeżenia działów). Tej zapewnionej jest przechowywany poza centrum danych firmowych kontrolowane hello i nie są pod kontrolą fizycznych hello firmy.

### <a name="company-goal"></a>Celem firmy

W ramach strategii zabezpieczeń obrony zabezpieczeń wielowarstwowy jest tooensure celem firmy, czy wszystkie źródła danych, które zawierają dane osobowe użytkownika są szyfrowane, łącznie z tymi znajdującymi się w magazynie w chmurze. Jeśli nieautoryzowany danych osobowych toohello dostępu korzyści osób, musi należeć do formularza, który będzie renderowany go nie można go odczytać. Zastosowanie szyfrowania powinna być łatwa lub przezroczyste — dla użytkowników i administratorów.

## <a name="solutions"></a>Rozwiązania

Usługi platformy Azure zapewniają wiele toohelp narzędzia i technologie ochrony danych osobowych w stanie spoczynku szyfrując go.

### <a name="azure-key-vault"></a>W usłudze Azure Key Vault

[Usługa Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) zapewnia bezpieczny magazyn kluczy hello używać tooencrypt danych przechowywanych w usługach Azure i hello zaleca klucza rozwiązanie pamięci masowej i zarządzania. Zarządzanie kluczami szyfrowania jest istotne toosecuring przechowywanych danych.

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>Jak używać usługi Azure Key Vault tooprotect klucze szyfrowania danych osobowych?

toouse usługi Azure Key Vault, należy tooan subskrypcji konto platformy Azure. Należy również zainstalować programu Azure PowerShell. Kroki obejmują przy użyciu następujących hello toodo poleceń cmdlet programu PowerShell:

1. Połącz tooyour subskrypcji

2. Tworzenie magazynu kluczy

3. Dodawanie klucza lub magazynu kluczy tajnych toohello

4. Rejestrowanie aplikacji używających magazynu kluczy hello usłudze Azure Active Directory

5. Autoryzowanie hello aplikacji toouse hello klucza lub klucza tajnego

toocreate magazyn kluczy, użyj polecenia cmdlet programu PowerShell New-AzureRmKeyVault hello. Przypisze nazwę magazynu, nazwa grupy zasobów i lokalizacji geograficznej. Nazwa magazynu hello będą używane podczas zarządzania kluczami za pośrednictwem innych poleceń cmdlet. Aplikacje używające magazynu hello za pomocą interfejsu API REST hello użyje magazynu hello identyfikatora URI.

Usługa Azure Key Vault zapewniają klucza chronionego przez oprogramowanie dla Ciebie lub zaimportować istniejący klucz w. Plik PFX. W magazynie hello można przechowywać klucze tajne (hasła).

Można również wygenerowanie klucza w lokalnym module HSM i przenieść tooHSMs w hello usługi Key Vault bez opuszczania hello granic modułu HSM klucz hello.

Aby uzyskać szczegółowe instrukcje na temat używania usługi Azure Key Vault, wykonaj hello kroki opisane w temacie [wprowadzenie do usługi Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

Aby uzyskać listę poleceń cmdlet programu PowerShell używane z usługą Azure Key Vault, zobacz [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

### <a name="azure-disk-encryption-for-windows"></a>Szyfrowanie dysków Azure dla systemu Windows

[Azure szyfrowania dysku dla systemu Windows i maszyn wirtualnych systemu Linux IaaS](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) chroni dane osobowe magazynowane na maszynach wirtualnych Azure i integruje się z usługą Azure Key Vault. Używa szyfrowania dysków Azure [funkcji BitLocker](https://technet.microsoft.com/library/cc732774.aspx) w systemie Windows i [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) w systemie Linux tooencrypt hello zarówno systemu operacyjnego i hello dysków danych. Szyfrowanie dysków Azure jest obsługiwana na Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 i na klientach z systemem Windows 8 i Windows 10.

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>Jak używać danych osobowych tooprotect szyfrowania dysków Azure?

toouse szyfrowania dysków Azure należy tooan subskrypcji konto platformy Azure. tooenable Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux, hello następujące:

1. Użyj hello Azure dysku szyfrowania szablonu usługi Resource Manager, programu PowerShell lub szyfrowanie dysków tooenable interfejsu wiersza polecenia (CLI) hello i określ konfiguracji szyfrowania. 

2. Udziel dostępu toohello platformy Azure tooread hello szyfrowania materiału z magazynu kluczy.

3. Podaj Azure Active Directory (AAD) aplikacji tożsamości toowrite hello szyfrowania tooyour materiału klucza magazynu kluczy.

Azure hello maszyny Wirtualnej i konfiguracji magazynu kluczy hello aktualizacji i skonfiguruj zaszyfrowanych maszyny Wirtualnej.

Po skonfigurowaniu toosupport Twojego magazynu kluczy szyfrowania dysków Azure można dodać klucza szyfrowania klucza (KEK), bezpieczeństwa i toosupport kopii zapasowej zaszyfrowanego maszyn wirtualnych.

![](media/protect-personal-data-at-rest/create-key.png)

Szczegółowe instrukcje dotyczące scenariuszy wdrażania i możliwości użytkowników znajdują się w [Azure dysku szyfrowanie dla systemu Windows i maszyn wirtualnych systemu Linux IaaS.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="azure-storage-service-encryption"></a>Szyfrowanie usługi Azure Storage

[Azure magazynu usługi szyfrowania (SSE) dla danych magazynowanych](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) pomaga chronić i chronić Twoje toomeet danych Twojej organizacji zobowiązań zabezpieczeń i zgodności. Magazyn Azure automatycznie szyfruje dane przy użyciu toostorage toopersisting wcześniejsze szyfrowania AES 256-bitowego i odszyfrowuje je, tooretrieval wcześniejsze. Ta usługa jest dostępna dla obiektów blob Azure i plików.

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>Jak używać danych osobowych tooprotect szyfrowanie usługi Magazyn?

tooenable szyfrowanie usługi Magazyn, hello następujące:

1. Zaloguj się do hello portalu Azure.

2. Wybierz konto magazynu.

3. W obszarze Ustawienia w sekcji usługa Blob hello, wybierz szyfrowania.

4. W obszarze hello sekcji usługi plików wybierz szyfrowania.

Po kliknięciu ustawienie szyfrowania hello, można włączyć lub wyłączyć szyfrowanie usługi magazynu.

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

Nowe dane będą szyfrowane. Dane w istniejących plików z tego konta magazynu pozostaną niezaszyfrowane.

Po włączeniu szyfrowania, skopiuj konto magazynu toohello danych przy użyciu jednej z następujących metod hello:

1. Kopiowanie obiektów blob lub pliki z hello [narzędzia wiersza polecenia AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).

2. [Instalowanie udziału plików, za pomocą protokołu SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) , można użyć narzędzia, takich jak pliki toocopy Robocopy.

3. Kopiowanie pliku lub obiektu blob danych tooand z magazynu obiektów blob lub między magazynu kont przy użyciu narzędzia [biblioteki klienta magazynu, takich jak .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).

4.  Użyj [Eksploratora usługi Storage](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooyour konta magazynu obiektów blob tooupload z włączone szyfrowanie.

### <a name="transparent-data-encryption"></a>Przezroczyste szyfrowanie danych

Funkcji przezroczystego szyfrowania danych (TDE) jest funkcją w usługach SQL Azure za pomocą którego można zaszyfrować dane na poziomie zarówno hello bazy danych i serwera. Funkcji TDE jest teraz włączone domyślnie na wszystkie nowo utworzone bazy danych. Funkcji TDE wykonuje w czasie rzeczywistym we/wy szyfrowanie i odszyfrowywanie hello plików danych i dziennika.

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>Jak używać funkcji TDE tooprotect osobistych danych?

Za pomocą hello interfejsu API REST lub przy użyciu programu PowerShell, można skonfigurować funkcji TDE za pośrednictwem hello portalu Azure. tooenable funkcji TDE na istniejącej bazy danych przy użyciu hello Azure Portal hello następujące:

1. Odwiedź hello Azure w portalu <https://portal.azure.com> i zaloguj się przy użyciu konta administratora platformy Azure lub współautora.

2. Na transparencie po lewej stronie powitania kliknij tooBROWSE, a następnie kliknij bazy danych SQL.

3. W okienku po lewej stronie powitania bazy danych SQL kliknij bazy danych użytkowników.

4. W bloku bazy danych hello kliknij pozycję wszystkie ustawienia.

5. W bloku ustawienia powitania kliknij danych przezroczystego szyfrowania części tooopen hello danych przezroczystego szyfrowania blok.

6. W bloku szyfrowania danych hello, Przenieś tooOn przycisk szyfrowania danych hello, a następnie kliknij Zapisz (u góry hello strony hello) tooapply hello ustawienie. Witaj stanu szyfrowania będzie przybliżona hello postęp hello przezroczystego szyfrowania danych.

![Włączanie szyfrowania danych](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

Instrukcje dotyczące sposobu tooenable funkcji TDE i informacji na temat odszyfrowywania chronionych funkcji TDE baz danych i inne można znaleźć w artykule hello [przezroczystego szyfrowania danych z bazy danych SQL Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>Podsumowanie

Witaj firmy można wykonywać jego celem szyfrowania danych osobowych przechowywanych w hello chmury Azure. Można to zrobić za pomocą szyfrowania dysków Azure zbyt chronić całą woluminów. Może to obejmować zarówno hello pliki systemu operacyjnego, jak i plików danych, które zawierają dane osobowe i innych poufnych danych. Szyfrowanie usługi Magazyn Azure mogą być używane tooprotect danych osobowych, które są przechowywane w plikach i obiektów blob. W przypadku danych przechowywanych w bazach danych Azure SQL przezroczystego szyfrowania danych zapewnia ochronę przed nieautoryzowanym ujawnienia informacji osobistych.

tooprotect hello kluczy, które są używane tooencrypt danych na platformie Azure, hello firmy można używać usługi Azure Key Vault. Usprawnia to proces zarządzania kluczami hello i umożliwia hello firmy toomaintain kontrolę nad kluczami, które dostępu i szyfrowanie danych osobowych.

## <a name="next-steps"></a>Następne kroki

- [Przewodnik rozwiązywania problemów szyfrowania dysków Azure](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [Szyfrowanie maszyny wirtualnej platformy Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Szyfrowanie danych w usłudze Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [Azure DB rozwiązania Cosmos szyfrowania bazy danych w stanie spoczynku](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
