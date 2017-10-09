---
title: "aaaAzure funkcji chmury powłoki (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Omówienie funkcji powłoki chmury Azure"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Funkcje i narzędzia dla chmury Azure powłoki
Powłoka chmury Azure jest toomanage środowisko powłoki przeglądarki i tworzenie zasobów Azure.

Chmura powłoki oferuje przeglądarki dostępny, wstępnie skonfigurowane środowisko powłoki zarządzania zasobami Azure bez zwiększania hello instalacja, przechowywanie wersji i obsługa maszynę, samodzielnie.

Powłoka chmury udostępnia maszyn, na podstawie żądań i w związku z tym maszyny stanu nie będzie zachowywane między sesjami. Ponieważ powłoki chmury jest skompilowany dla sesji interaktywne, powłok automatycznie usunięte po upływie 20 minut braku aktywności powłoki.

## <a name="bash-in-cloud-shell"></a>Bash w powłoce chmury
### <a name="tools"></a>Narzędzia
|Kategoria   |Nazwa   |
|---|---|
|Interpreter powłoki systemu Linux|Bash<br> Pokaż               |
|Narzędzia platformy Azure            |[Azure CLI 2.0](https://github.com/Azure/azure-cli) i [1.0](https://github.com/Azure/azure-xplat-cli)<br> [Narzędzie AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Usługa Batch Shipyard](https://github.com/Azure/batch-shipyard)     |
|Edytory tekstów           |VIM<br> nano<br> emacs:       |
|Kontrola źródła         |git                    |
|Narzędzi do kompilacji            |Wprowadź<br> maven<br> npm<br> PIP         |
|Kontenery             |[Interfejs wiersza polecenia docker](https://github.com/docker/cli)/[Docker maszyny](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Projekt](https://github.com/Azure/draft)<br> [INTERFEJS WIERSZA POLECENIA DC/OS](https://github.com/dcos/dcos-cli)         |
|Bazy danych              |Klienta MySQL<br> PostgreSql klienta<br> [Narzędzia sqlcmd](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [Autorzy MSSQL skryptów](https://github.com/Microsoft/sql-xplat-cli) |
|Inne                  |iPython klienta<br> [Chmura Foundry interfejsu wiersza polecenia](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a>Obsługa języków
|Język   |Wersja   |
|---|---|
|.NET       |1.01       |
|Przejdź         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 i 3.5 (ustawienie domyślne)|

## <a name="secure-automatic-authentication"></a>Bezpieczne uwierzytelnianie automatyczne
Chmury powłoki bezpiecznie i automatycznie uwierzytelnia dostęp konta dla hello Azure CLI 2.0.

## <a name="azure-files-persistence"></a>Azure trwałości plików
Ponieważ powłoki w chmurze jest przydzielony dla danego żądania przy użyciu tymczasowej maszyny, pliki poza Twojej $Home i maszyny stanu nie są zachowywane między sesjami.
pliki toopersist między sesjami, przeszukiwań powłoki w chmurze za pośrednictwem dołączanie plików na platformę Azure udostępniania przy pierwszym uruchomieniu.
Po zakończeniu powłoki chmury dołączać automatycznie magazynu dla wszystkich przyszłych sesji.

[Dowiedz się więcej na temat dołączania tooCloud udziałów plików na platformę Azure powłoki.](persisting-shell-storage.md)

## <a name="next-steps"></a>Następne kroki
[Szybki Start powłoki chmury](quickstart.md) <br>
[Więcej informacji na temat usługi Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) <br>