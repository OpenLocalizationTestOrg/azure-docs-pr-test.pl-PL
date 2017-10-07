---
title: "Rozwiązywanie problemów z działanie usługi Azure Active Directory rejestruje błędy pakiet zawartości | Dokumentacja firmy Microsoft"
description: "Zawiera listę komunikatów o błędach programu hello działanie usługi Azure Active Directory zawartości pakietu i kroki toofix je."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Rozwiązywanie problemów z działanie usługi Azure Active Directory rejestruje błędy pakiet zawartości 


Podczas pracy z hello pakiet zawartości Power BI dla wersji zapoznawczej usługi Azure Active Directory, możliwe jest funkcjonowaniem hello następujące błędy: 

- [Odświeżanie nie powiodło się](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [Poświadczenia źródła danych nie powiodło się tooupdate](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [Importowanie danych trwa zbyt długo](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
Ten temat zawiera informacje o hello możliwe przyczyny i w jaki sposób toofix te błędy.
 
## <a name="refresh-failed"></a>Odświeżanie nie powiodło się 
 
**Sposób ten błąd jest udostępniane**: wiadomości E-mail z usługi Power BI lub stan niepowodzenia w historii odświeżania hello. 


| Przyczyna | Jak toofix |
| ---   | ---        |
| Odśwież awarii błędy może być spowodowany hello poświadczeń użytkowników hello łączenie pakiet zawartości toohello zostały resetowania, ale nie zostały zaktualizowane w ustawieniach połączenia hello hello hello pakietu zawartości. | W usłudze Power BI zlokalizować odpowiednich toohello dataset hello pulpitu nawigacyjnego dzienniki działanie usługi Azure Active Directory (Dzienniki działanie usługi Azure Active Directory), wybierz pozycję harmonogram odświeżania, a następnie wprowadź poświadczenia usługi Azure AD. |
| Odświeżanie może zakończyć się niepowodzeniem ze względu na problemy toodata w hello bazowy pakiet zawartości. | Plik biletu pomocy technicznej. Aby uzyskać więcej informacji, zobacz [jak tooget obsługują usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>Poświadczenia źródła danych nie powiodło się tooupdate 
 
**Sposób ten błąd jest udostępniane**: W usłudze Power BI, łącząc toohello pakiet zawartości dzienników (wersja zapoznawcza) działanie usługi Azure Active Directory. 

| Przyczyna | Jak toofix |
| ---   | ---        |
| użytkownik nawiązujący połączenie Hello jest administratorem globalnym, ani czytnika zabezpieczeń ani administratora zabezpieczeń. | Użyj konta, które jest administratorem globalnym lub czytnik zabezpieczeń lub zabezpieczeń administratora tooaccess hello pakietów zawartości. |
| Dzierżawy nie jest dzierżawa usługi Premium lub nie ma co najmniej jednego użytkownika z licencją Premium pliku. | Plik biletu pomocy technicznej. Aby uzyskać więcej informacji, zobacz [jak tooget obsługują usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>Importowanie danych trwa zbyt długo 
 
**Sposób ten błąd jest udostępniane**: W usłudze Power BI, po połączeniu pakietu zawartości, proces importowania danych hello uruchamia tooprepare pulpitu nawigacyjnego dla dziennika działanie usługi Azure Active Directory. Zobacz wiadomość hello: "*importowania danych...* "  

| Przyczyna | Jak toofix |
| ---   | ---        |
| W zależności od rozmiaru hello dzierżawy ten krok może zająć od kilku minut too30 minut. | Właśnie o cierpliwość. Jeśli wiadomość hello nie zmienia tooshowing pulpitu nawigacyjnego w ciągu jednej godziny, zgłoś biletu pomocy technicznej. Aby uzyskać więcej informacji, zobacz [jak tooget obsługują usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).|

## <a name="next-steps"></a>Następne kroki

Witaj tooinstall pakiet zawartości Power BI dla Azure Active Directory w wersji zapoznawczej, kliknij przycisk [tutaj](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).


