---
title: informacje o wersji aaaAzure Data Catalog | Dokumentacja firmy Microsoft
description: "Informacje o wersji dla usługi Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Informacje o wersji usługi Azure Data Catalog
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Informacje o wersji 20 listopada 2015 hello Azure Data Catalog
### <a name="opening-data-sources-in-power-bi-desktop"></a>Otwieranie źródeł danych w programie Power BI Desktop
Korzystając z opcji "Otwórz w Power BI Desktop" hello z hello **Azure Data Catalog** portalu, użytkownicy mogą wystąpić jeden z dwóch problemów w aplikacji Power BI Desktop hello:

* Zostanie wyświetlone okno dialogowe, z tytułem hello "TooOpen dokumentu"
* Otwiera Hello aplikacji Power BI Desktop, ale plik hello pojawi się pusta toobe

W każdej sytuacji hello problemu przez pobranie i zainstalowanie najnowszej wersji programu Power BI Desktop z hello [witryny PowerBI.com](https://powerbi.com).

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Informacje o wersji 13 listopada 2015 hello Azure Data Catalog
### <a name="registering-and-connecting-tooteradata"></a>Rejestrowanie i łączenie tooTeradata
Łącząc tooTeradata źródeł danych użytkownicy mają zainstalowany sterownik Teradata ODBC hello, które odpowiada hello liczbie bitów (32-bitowy lub 64-bitowy) hello oprogramowanie wykorzystywane.

Począwszy od tej ADC Data wydania, hello najnowszych [sterownika ODBC programu Teradata dla systemu windows (wersja 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) jest zgodny z pakietu Office 2013, ale nie z pakietu Office 2016.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Informacje o wersji 13 lipca 2015 hello Azure Data Catalog
### <a name="registering-and-connecting-toooracle-database"></a>Rejestrowanie i łączenie tooOracle bazy danych
Podczas łączenia użytkowników źródeł danych bazy danych tooOracle musi być zainstalowany hello poprawne Oracle sterowniki zgodne hello liczba bitów (32-bitowy lub 64-bitowy) hello oprogramowanie wykorzystywane.

* Podczas rejestrowania źródła danych Oracle na komputerze z 32-bitowego systemu Windows, będą używane hello 32-bitowe sterowniki Oracle
* Podczas rejestrowania źródła danych Oracle na komputerze z systemem 64-bitowego systemu Windows, będą używane hello 64-bitowych Oracle sterowników
* Podczas łączenia z tooOracle źródła danych przy użyciu programu Excel na komputerze z systemem hello 32-bitowej wersji pakietu Microsoft Office, w tym na 64-bitowej wersji systemu Windows hello 32-bitowe sterowniki Oracle będą używane
* Podczas łączenia z tooOracle źródła danych przy użyciu programu Excel na komputerze z systemem hello 64-bitowej wersji pakietu Microsoft Office, będą używane hello 64-bitowych Oracle sterowników

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>Rejestrowanie i łączenie tooSQL Server Reporting Services
Obsługa źródeł danych usługi SQL Server Reporting Services (SSRS) jest obecnie ograniczone tooNative tryb tylko serwerów. Obsługa usługi SSRS w trybie programu SharePoint zostanie dodany w nowszej wersji.

### <a name="opening-data-assets-in-excel"></a>Otwieranie zasobów danych w programie Excel
Podczas otwierania zasobów danych w programie Microsoft Excel z hello **Azure Data Catalog** portalu użytkowników może zostać wyświetlony monit o **powiadomienie o zabezpieczeniach programu Microsoft Excel** okno dialogowe. Standard, jest to oczekiwane zachowanie, a użytkownicy mogą wybrać **włączyć** toocontinue.

Aby uzyskać więcej informacji, zobacz [Włącz lub Wyłącz alerty zabezpieczeń dotyczące łącza i pliki z podejrzanych witrynach internetowych](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Serwer proxy i zasad konfiguracji i danych rejestracji źródła
Użytkownicy mogą wystąpić w sytuacji, w którym można rejestrować na toohello portalu wykazu danych Azure, ale podczas prób toolog na toohello narzędzia rejestracji źródła danych w momencie napotkania komunikat o błędzie, który uniemożliwia zalogowanie.

Istnieją dwie możliwe przyczyny tego problemu zachowania:

**1 Przyczyna: Konfiguracja Active Directory Federation Services** narzędzia rejestracji źródła danych hello korzysta z uwierzytelniania formularzy toovalidate użytkownika logowania do usługi Active Directory. Do pomyślnego logowania należy włączyć uwierzytelnianie formularzy w hello globalne zasady uwierzytelniania przez administratora usługi Active Directory.

W niektórych sytuacjach zachowanie ten błąd może wystąpić tylko wtedy, gdy użytkownik hello znajduje się w sieci firmy hello lub tylko wtedy, gdy użytkownik hello nawiązuje połączenie z hello poza siecią firmową. Witaj globalne zasady uwierzytelniania umożliwia włączone oddzielnie w intranecie i ekstranecie połączeń toobe metody uwierzytelniania. Błędy logowania może wystąpić, jeśli nie włączono uwierzytelniania formularzy hello sieci, z których hello użytkownik nawiązuje połączenie.

Aby uzyskać więcej informacji, zobacz [Konfigurowanie zasad uwierzytelniania](https://technet.microsoft.com/library/dn486781.aspx).

**Przyczyny 2: Konfiguracja serwera proxy sieci** Jeśli hello sieć firmowa używa serwera proxy, narzędzie rejestracji hello może nie być możliwe tooconnect tooAzure usługi Active Directory za pośrednictwem serwera proxy hello. Użytkownicy zapewnia narzędzia rejestracji hello, edytując plik konfiguracji narzędzia hello, dodawanie tego pliku toohello sekcji:

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


toolocate hello RegistrationTool.exe.config plików, uruchom narzędzie rejestracji hello, a następnie otwórz narzędzie Menedżera zadań systemu Windows hello. Na karcie Szczegóły hello w Menedżerze zadań kliknij prawym przyciskiem myszy na RegistrationTool.exe i wybierz z menu podręcznego hello Otwórz lokalizację pliku.
