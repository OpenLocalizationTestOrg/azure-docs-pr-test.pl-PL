---
title: "Pulpit zdalny przy użyciu ról Azure aaaUsing | Dokumentacja firmy Microsoft"
description: "Przy użyciu pulpitu zdalnego z rolami systemu Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a>Przy użyciu pulpitu zdalnego z rolami systemu Azure
Przy użyciu hello zestawu SDK platformy Azure i usługi pulpitu zdalnego, można uzyskać dostępu do ról platformy Azure i maszyn wirtualnych, które są obsługiwane przez platformę Azure. W programie Visual Studio można skonfigurować usługi pulpitu zdalnego z projektu usługi w chmurze Azure. tooenable usług pulpitu zdalnego, musisz utworzyć projekt pracy, który zawiera co najmniej jedną rolę, a następnie opublikować go tooAzure.

> [!IMPORTANT]
> Możesz uzyskać dostęp Azure roli do rozwiązywania problemów lub tylko programowanie. Witaj przeznaczenie każdej maszyny wirtualnej jest toorun konkretnej roli w aplikacji platformy Azure, nie toorun inne aplikacje klienckie. Jeśli chcesz toouse toohost Azure maszyny wirtualnej, która służy do celów, zobacz Uzyskiwanie dostępu do maszyn wirtualnych platformy Azure z poziomu Eksploratora serwera.
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a>tooenable i użyj pulpitu zdalnego dla roli Azure
1. W Eksploratorze rozwiązań Otwórz menu skrótów hello projekt usługi w chmurze, a następnie wybierz **publikowania**.
   
    Witaj **publikowanie aplikacji platformy Azure** zostanie wyświetlony Kreator.
   
    ![Publikowanie polecenia dla projektu usługi w chmurze](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. U dołu hello **ustawień publikowania platformy Azure Microsoft** hello kreatora wybierz hello **Włącz pulpit zdalny** wszystkie pola wyboru ról. 
   
    Witaj **konfigurację usług pulpitu zdalnego** zostanie wyświetlone okno dialogowe.
3. U dołu hello hello **konfigurację usług pulpitu zdalnego** oknie dialogowym Wybierz hello **więcej opcji** przycisku. 
   
    Zostaną wyświetlone pole listy rozwijanej, które można tworzyć lub wybrać certyfikat, dzięki czemu można zaszyfrować informacji poświadczeń przy nawiązywaniu połączeń za pośrednictwem pulpitu zdalnego.
4. Z listy rozwijanej hello wybierz  **&lt;Utwórz >**, lub wybierz istniejący z listy hello. 
   
    Jeśli wybierzesz istniejącego certyfikatu, Pomiń hello następujące kroki.
   
   > [!NOTE]
   > Hello certyfikaty, które należy do podłączania pulpitu zdalnego są inne niż hello certyfikaty, które są używane dla innych operacji platformy Azure. Witaj certyfikat dostępu zdalnego musi mieć klucz prywatny.
   > 
   > 
   
    Witaj **Tworzenie certyfikatu** zostanie wyświetlone okno dialogowe.
   
   1. Podaj przyjazną nazwę dla nowego certyfikatu hello, a następnie wybierz hello **OK** przycisku. w polu listy rozwijanej hello pojawi się Hello nowego certyfikatu.
   2. W hello **konfigurację usług pulpitu zdalnego** okna dialogowego wprowadź nazwę użytkownika i hasło.
      
       Nie można użyć istniejącego konta. Nie można określić administratora hello nazwy użytkownika dla nowego konta hello.
      
      > [!NOTE]
      > Jeśli hello hasło nie spełnia wymagań dotyczących złożoności hello, czerwona ikona pojawi się pole tekstowe hasła toohello dalej. Witaj hasło musi zawierać wielkie litery, małe litery i liczby lub symbole.
      > 
      > 
   3. Wybierz datę na konto, które hello wygasną i po którym połączeń pulpitu zdalnego zostanie zablokowana.
   4. Po, które zostały podane hello wszystkie wymagane informacje, wybierz hello **OK** przycisku.
      
       Wiele ustawień, które umożliwiają dostęp zdalny są dodawane toohello plików cscfg i csdef.
5. W hello **ustawień publikowania platformy Azure Microsoft** kreatora wybierz hello **OK** przycisku, gdy wszystko jest gotowe toopublish usługi w chmurze.
   
    Jeśli nie masz toopublish gotowe, wybierz hello **anulować** przycisku. ustawienia konfiguracji Hello są zapisywane, a później można opublikować usługi w chmurze.

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a>Połącz tooan roli Azure przy użyciu pulpitu zdalnego
Po opublikowaniu usługi w chmurze na platformie Azure umożliwia toolog Eksploratora serwera na powitania maszyny wirtualnej obsługującego Azure. 

1. W Eksploratorze serwera rozwiń hello **Azure** węzeł, a następnie rozwiń węzeł hello usługi w chmurze i jeden z jej ról toodisplay listę wystąpień.
2. Otwórz menu skrótów hello węzła wystąpienia, a następnie wybierz **połączyć za pomocą pulpitu zdalnego**.
   
    ![Łączenie za pośrednictwem pulpitu zdalnego](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. Wprowadź hello nazwy użytkownika i hasła, utworzony wcześniej. Obecnie użytkownik jest zalogowany do sesji zdalnej.

