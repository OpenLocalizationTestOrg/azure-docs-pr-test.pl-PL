---
title: "aaaGet danych przy użyciu hello Azure AD interfejsu API raportowania z certyfikatami | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak toouse hello Azure AD interfejsu API raportowania certyfikat poświadczeń tooget danymi z katalogów bez interwencji użytkownika."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>Pobierz dane przy użyciu interfejsu API raportowania usługi Azure AD hello z certyfikatami
W tym artykule opisano, jak toouse hello Azure AD interfejsu API raportowania certyfikat poświadczeń tooget danymi z katalogów bez interwencji użytkownika. 

## <a name="use-hello-azure-ad-reporting-api"></a>Użyj hello Azure AD interfejsu API raportowania 
Azure AD interfejsu API raportowania wymaga wykonanie hello następujące kroki:
 *  Instalacja wymagań wstępnych
 *  Ustaw hello certyfikatu w aplikacji
 *  Pobranie tokenu dostępu
 *  Użyj hello toocall tokenu dostępu hello interfejsu API programu Graph

Aby uzyskać informacje o kodzie źródłowym, zobacz [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Wykorzystanie modułu interfejsu API raportowania). 

### <a name="install-prerequisites"></a>Instalacja wymagań wstępnych
Konieczne będzie toohave programu Azure AD PowerShell V2 i zainstalowany moduł AzureADUtils.

1. Pobieranie i instalowanie programu Azure AD Powershell V2, postępując zgodnie z instrukcjami hello na [środowiska PowerShell usługi Azure Active Directory](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).
2. Pobierz moduł Azure AD witryny hello z [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1). 
  Ten moduł zapewnia kilka poleceń cmdlet narzędzi, w tym:
   * Witaj najnowszej wersji biblioteki adal przy użyciu narzędzia Nuget
   * Tokeny dostępu użytkownika, kluczy aplikacji i certyfikatów korzystających z bibliotek ADAL
   * Stronicowane wyniki obsługi interfejsu API programu Graph

**Moduł Azure AD witryny hello tooinstall:**

1. Utwórz moduł narzędzia hello toosave katalog (na przykład c:\azureAD) i Pobierz hello modułu z usługi GitHub.
2. Otwórz sesję programu PowerShell, a następnie przejdź do katalogu toohello, który został utworzony. 
3. Zaimportuj moduł hello i zainstaluj go w ścieżce modułu programu PowerShell hello przy użyciu polecenia cmdlet hello AzureADUtilsModule instalacji. 

Hello sesji powinien wyglądać podobnie toothis ekranu:

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>Ustaw hello certyfikatu w aplikacji
1. Jeśli już masz aplikację, należy pobrać Identyfikatora obiektu z hello portalu Azure. 

  ![Azure Portal](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. Otwórz sesję programu PowerShell i połącz tooAzure AD za pomocą polecenia cmdlet Connect-AzureAD hello.

  ![Azure Portal](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. Użyj polecenia cmdlet New-AzureADApplicationCertificateCredential hello tooadd AzureADUtils tooit poświadczenie certyfikatu. 

>[!Note]
>Możesz muszą aplikacji hello tooprovide Identyfikatora obiektu, która została przechwycona wcześniej, a także hello obiektu certyfikatu (przy użyciu tego hello Cert: dysk).
>


  ![Azure Portal](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>Pobranie tokenu dostępu

tooget tokenu dostępu, użyj polecenia cmdlet Get-AzureADGraphAPIAccessTokenFromCert hello AzureADUtils. 

>[!NOTE]
>Należy toouse hello identyfikator aplikacji zamiast hello Identyfikatora obiektu, który został użyty w ostatniej sekcji hello.
>

 ![Azure Portal](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Użyj hello toocall tokenu dostępu hello interfejsu API programu Graph

Teraz możesz utworzyć hello skryptu. Poniżej przedstawiono przykład za pomocą polecenia cmdlet Invoke-AzureADGraphAPIQuery hello hello AzureADUtils. To polecenie cmdlet obsługuje wyników wielu stronicowania, a następnie wysyła te wyniki toohello PowerShell potoku. 

 ![Azure Portal](./media/active-directory-report-api-with-certificates/script-completed.png)

Są teraz gotowe tooexport tooa CSV i zapisać tooa SIEM system. Można również zawijać skryptu w tooget zaplanowane zadanie danych usługi Azure AD z dzierżawą okresowo bez konieczności toostore kluczy aplikacji hello kodu źródłowego. 

## <a name="next-steps"></a>Następne kroki
[Witaj podstawowe informacje na temat zarządzania tożsamość platformy Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



