---
title: "Konto usługi Automatyzacja Azure aaaManage | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toomanage hello konfiguracji Twoje konto usługi Automatyzacja, takie jak odnawiania certyfikatu, usuwanie i błędnej konfiguracji."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a>Zarządzanie kontem usługi Azure Automation
W pewnym momencie przed upływem Twoje konto usługi Automatyzacja, konieczne będzie toorenew hello certyfikatu. Jeśli uważasz, że naruszono tego hello konta Uruchom jako, można usunąć i ponownie go utworzyć. W tej sekcji omówiono sposób tooperform te operacje.

## <a name="self-signed-certificate-renewal"></a>Odnawianie certyfikatu z podpisem własnym
Witaj podpisem utworzony certyfikat dla hello konta Uruchom jako wygasa rok z daty utworzenia hello. Można go odnowić w dowolnym momencie przed wygaśnięciem jego ważności. Podczas odnawiania go hello bieżącego prawidłowy certyfikat jest zachowanych tooensure, że wszystkie elementy runbook umieszczonych w kolejce maksymalnie lub aktywnie działa i że uwierzytelniania za pomocą hello konta Uruchom jako nie negatywnie zainfekowane. certyfikat Hello pozostaje ważny aż do daty jego wygaśnięcia.

> [!NOTE]
> Jeśli zostały skonfigurowane z automatyzacji Uruchom jako konta toouse certyfikat wystawiony przez urząd certyfikacji w Twojej organizacji, możesz użyć tej opcji hello firmowy certyfikat zostanie zastąpione przez certyfikatu z podpisem własnym.

Witaj toorenew certyfikatów, hello następujące:

1. Hello portalu Azure Otwórz hello konta automatyzacji.

2. Na powitania **konto automatyzacji** bloku w hello **konta właściwości** okienku w obszarze **ustawienia konta**, wybierz pozycję **konta Uruchom jako**.

    ![Okienko właściwości konta usługi Automation](media/automation-manage-account/automation-account-properties-pane.png)
3. Na powitania **konta Uruchom jako** bloku właściwości, wybierz albo hello Uruchom jako konta lub hello klasycznego konto Uruchom jako ma toorenew hello certyfikat dla.

4. Na powitania **właściwości** bloku hello wybranego konta, kliknij przycisk **odnawiania certyfikatu**.

    ![Odnawianie certyfikatu konta Uruchom jako](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. Gdy hello certyfikat zostanie odnowiony, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.

## <a name="delete-a-run-as-or-classic-run-as-account"></a>Usuwanie konta Uruchom jako lub klasycznego konta Uruchom jako
W tej sekcji opisano sposób toodelete i ponownie utwórz konto Uruchom jako lub klasycznego Uruchom jako. Podczas wykonywania tej akcji jest zachowywana hello konta automatyzacji. Po usunięciu konta Uruchom jako lub klasycznego Uruchom jako, można go utworzyć ponownie w hello portalu Azure.

1. Hello portalu Azure Otwórz hello konta automatyzacji.

2. Na powitania **konto automatyzacji** bloku w hello konta w okienku właściwości, wybierz opcję **konta Uruchom jako**.

3. Na powitania **konta Uruchom jako** bloku właściwości, albo hello Uruchom jako konto klasycznego konto Uruchom jako lub wybierz konto, które mają toodelete. Następnie na powitania **właściwości** bloku hello wybranego konta, kliknij przycisk **usunąć**.

 ![Usuwanie konta Uruchom jako](media/automation-manage-account/automation-account-delete-runas.png)

4. Gdy konto hello jest usuwany, możesz śledzić postępy hello w obszarze **powiadomienia** hello menu.

5. Po usunięciu konta hello, można go ponownie utworzyć na powitania **konta Uruchom jako** opcja tworzenia bloku właściwości, wybierając hello **Azure konta Uruchom jako**.

 ![Ponownie utwórz konto Uruchom jako automatyzacji hello](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a>Błąd konfiguracji
Niektóre elementy konfiguracji niezbędne do toofunction konta Uruchom jako klasycznego konto Uruchom jako lub hello prawidłowo może zostały usunięte lub nieprawidłowo utworzone podczas instalacji początkowej. elementy Hello obejmują:

* Zasób certyfikatu
* Zasób połączenia
* Konto Uruchom jako zostało usunięte z hello roli współautora
* Nazwa główna usługi lub aplikacji w usłudze Azure AD

W poprzednim hello i inne wystąpienia błędnej konfiguracji hello konta automatyzacji wykrywa hello zmiany i ma stan *niepełnym* na powitania **konta Uruchom jako** bloku właściwości hello konto.

![Stan Niekompletne dla konfiguracji konta Uruchom jako](media/automation-manage-account/automation-account-runas-incomplete-config.png)

Po wybraniu konta Uruchom jako hello hello konta **właściwości** okienko zawierające hello następujący komunikat o błędzie:

![Komunikat ostrzegawczy Niekompletne dla konfiguracji konta Uruchom jako](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png).

Przez usunięcie i ponowne utworzenie konta hello można szybko rozwiązać te problemy Uruchom jako konta.

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać więcej informacji na temat nazwy główne usług można znaleźć zbyt[obiekty aplikacji i nazwy głównej usługi](../active-directory/active-directory-application-objects.md).
* Aby uzyskać więcej informacji na temat opartej na rolach kontroli dostępu w usłudze Automatyzacja Azure można znaleźć zbyt[kontroli dostępu opartej na rolach w automatyzacji Azure](automation-role-based-access-control.md).
* Aby uzyskać więcej informacji na temat certyfikatów i usług Azure można znaleźć zbyt[Omówienie certyfikatów dla usług w chmurze Azure](../cloud-services/cloud-services-certs-create.md).
