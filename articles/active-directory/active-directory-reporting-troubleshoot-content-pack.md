---
title: "Rozwiązywanie problemów z działanie usługi Azure Active Directory rejestruje błędy pakiet zawartości | Dokumentacja firmy Microsoft"
description: "Udostępnia listę komunikatów o błędach pakiet zawartości działanie usługi Azure Active Directory i kroki rozwiązywania tych problemów."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: mtillman
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: b22f387a0338246c7586f0f0735b4612a796691a
ms.sourcegitcommit: 384d2ec82214e8af0fc4891f9f840fb7cf89ef59
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/16/2018
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Rozwiązywanie problemów z działanie usługi Azure Active Directory rejestruje błędy pakiet zawartości 


Podczas pracy z pakiet zawartości Power BI dla wersji zapoznawczej usługi Azure Active Directory, możliwe jest wystąpiły następujące błędy: 

- [Odświeżanie nie powiodło się](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [Nie można zaktualizować poświadczeń źródła danych](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [Importowanie danych trwa zbyt długo](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
Ten temat zawiera informacje o możliwych przyczyn i jak te błędy.
 
## <a name="refresh-failed"></a>Odświeżanie nie powiodło się 
 
**Sposób ten błąd jest udostępniane**: wiadomości E-mail z usługi Power BI lub stan niepowodzenia w historii odświeżania. 


| Przyczyna | Jak rozwiązać |
| ---   | ---        |
| Odśwież awarii może być spowodowany błędy, gdy poświadczenia użytkowników łączących się pakiet zawartości zostały resetowania, ale nie zostały zaktualizowane w ustawieniach połączenia pakietu zawartości. | W usłudze Power BI zestawu danych odpowiadające pulpitu nawigacyjnego dzienniki działanie usługi Azure Active Directory (Dzienniki działanie usługi Azure Active Directory), wybierz pozycję harmonogram odświeżania, a następnie wprowadź poświadczenia usługi Azure AD. |
| Odświeżanie może zakończyć się niepowodzeniem z powodu problemów danych w podstawowej pakietu zawartości. | Plik biletu pomocy technicznej. Aby uzyskać więcej informacji, zobacz [jak uzyskać pomoc techniczną dotyczącą usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 
 
## <a name="failed-to-update-data-source-credentials"></a>Nie można zaktualizować poświadczeń źródła danych 
 
**Sposób ten błąd jest udostępniane**: W usłudze Power BI, jeśli łączysz się z pakietu zawartości dzienników (wersja zapoznawcza) działanie usługi Azure Active Directory. 

| Przyczyna | Jak rozwiązać |
| ---   | ---        |
| Użytkownik nawiązujący połączenie jest administratorem globalnym, ani czytnika zabezpieczeń ani administratora zabezpieczeń. | Użyj konta, które jest administratorem globalnym lub czytnik zabezpieczeń lub administratora zabezpieczeń można uzyskać dostępu do zawartości pakietów. |
| Dzierżawy nie jest dzierżawa usługi Premium lub nie ma co najmniej jednego użytkownika z licencją Premium pliku. | Plik biletu pomocy technicznej. Aby uzyskać więcej informacji, zobacz [jak uzyskać pomoc techniczną dotyczącą usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>Importowanie danych trwa zbyt długo 
 
**Sposób ten błąd jest udostępniane**: W usłudze Power BI, po połączeniu pakietu zawartości, proces importowania danych rozpoczyna się przygotować pulpitu nawigacyjnego dla dziennika działanie usługi Azure Active Directory. Zostanie wyświetlony komunikat: "*importowania danych...* "  

| Przyczyna | Jak rozwiązać |
| ---   | ---        |
| W zależności od wielkości dzierżawy ten krok może potrwać od w ciągu kilku minut do 30 minut. | Właśnie o cierpliwość. Jeśli wiadomość nie zmienia się na wyświetlanie pulpitu nawigacyjnego w ciągu jednej godziny, zgłoś biletu pomocy technicznej. Aby uzyskać więcej informacji, zobacz [jak uzyskać pomoc techniczną dotyczącą usługi Azure Active Directory](active-directory-troubleshooting-support-howto.md).|

## <a name="next-steps"></a>Kolejne kroki

Aby zainstalować pakiet zawartości Power BI dla wersji zapoznawczej usługi Azure Active Directory, kliknij przycisk [tutaj](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).


