---
title: "alerty zabezpieczeń tooconfigure aaaHow | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak alerty zabezpieczeń tooconfigure dla rozszerzenia Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a>Jak zabezpieczeń tooconfigure alerty w programie Azure AD Privileged Identity Management
## <a name="security-alerts"></a>Alerty zabezpieczeń
Azure Privileged Identity zarządzania (PIM) generuje alerty w przypadku podejrzanej lub niebezpieczna działania w danym środowisku. Po wyzwoleniu alertu jest wyświetlane na pulpicie nawigacyjnym usługi PIM hello. Wybierz toosee alertu hello raportu użytkowników lub ról, które wywołały hello alert tekst hello list.

![Alerty zabezpieczeń pulpitu nawigacyjnego PIM — zrzut ekranu][1]

| Alerty | Wyzwalacz | Zalecenie |
| --- | --- | --- |
| **Role są przypisywane poza usługą PIM** |Administrator trwale przypisano roli tooa, poza hello PIM interfejsu. |Przejrzyj hello nowe przypisanie roli. Ponieważ inne usługi można przypisać tylko administratorami trwałymi, zmienić go tooan kwalifikujących się przypisanie w razie potrzeby. |
| **Role są aktywowane zbyt często** |Znaleziono zbyt wiele reaktywacje o tej samej roli w czasie hello dozwolone w ustawieniach hello hello. |Skontaktuj się z toosee użytkownika hello Dlaczego ich uaktywniono rolę hello tak wiele razy. Może wymagać więcej czasu hello limit jest za krótka dla nich toocomplete korzystania z ich zadań lub może być one skrypty tooautomatically aktywować rolę. |
| **Role nie wymagają uwierzytelniania wieloskładnikowego w celu aktywacji** |Dostępne są role bez włączone w ustawieniach hello MFA. |Firma Microsoft uwierzytelniania MFA można wymagać dla ról hello najbardziej wysoce uprzywilejowane, ale zdecydowanie zaleca się włączenie usługi MFA do aktywacji wszystkich ról. |
| **Administratorzy nie są używane role uprzywilejowane** |Brak kwalifikujących się Administratorzy, które nie zostały ostatnio aktywowane ich ról. |Uruchom dostępu przeglądu toodetermine hello użytkowników, którzy nie potrzebują już dostępu. |
| **Istnieje zbyt wiele administratorów globalnych** |Brak administratorów globalnych niż zalecane. |Jeśli masz dużą liczbę administratorów globalnych, istnieje prawdopodobieństwo, że użytkownicy uzyskują więcej uprawnień niż jest to wymagane. Przenieś użytkowników tooless uprzywilejowany ról lub upewnij niektóre z nich kwalifikuje się do roli hello zamiast trwale przypisana. |

## <a name="configure-security-alert-settings"></a>Konfigurowanie ustawień alertów zabezpieczeń
Niektóre alerty zabezpieczeń hello w toowork PIM środowiska i cele zabezpieczeń można dostosować. Wykonaj te kroki tooreach hello ustawienia bloku:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) i wybierz hello **Azure AD Privileged Identity Management** Kafelek z hello pulpitu nawigacyjnego.
2. Wybierz **zarządzane ról uprzywilejowanych** > **ustawienia** > **alerty ustawienia**.
   
    ![Przejdź do ustawień alertów toosecurity][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>Alert "Role są aktywowane zbyt często"
Ten alert, wyzwalacze, jeśli użytkownik aktywuje hello tej samej roli uprzywilejowanej wiele razy w danym okresie. Możesz skonfigurować zarówno hello czas okresu i hello liczbę aktywacji.

* **Okres odnawiania aktywacji**: Określ w dni, godziny, minuty, a po raz drugi hello okresu ma toouse tootrack podejrzane odnowienia.
* **Liczba odnowień aktywacji**: Określ hello liczbę aktywacji z too100 2, które należy wziąć pod uwagę warta alertu w przedziale czasu hello została wybrana opcja. Można zmienić to ustawienie przez przenoszenie suwaka hello, lub wpisz liczbę w polu tekstowym hello.

### <a name="there-are-too-many-global-administrators-alert"></a>Alert "są zbyt wielu administratorów globalnych"
PIM wyzwala ten alert, jeśli są spełnione dwa różne kryteria, a obie z nich można skonfigurować. Najpierw należy tooreach pewnej wartości progowej administratorów globalnych. Po drugie określonego procentu przypisania roli całkowita musi być administratorów globalnych. Jeśli tylko spełnia jednego z tych wskaźników, hello alertu nie jest widoczna.  

* **Minimalna liczba administratorów globalnych**: Określ hello liczba administratorów globalnych z too100 2, należy rozważyć kwotę niebezpieczne.
* **Procent administratorów globalnych**: Określ hello procent administratorów, którzy mają Administratorzy globalni od 0% too100%, która jest niebezpieczne w danym środowisku.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>Alert "Administratorzy nie są używane role uprzywilejowane"
Ten alert wyzwala, jeśli użytkownik przejdzie do pewnego czasu bez uaktywniania roli.

* **Liczba dni**: Określ hello liczbę dni od too100 0, który użytkownik może przejść bez uaktywniania roli.

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
