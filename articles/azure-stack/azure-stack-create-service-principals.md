---
title: "Tworzenie nazwy głównej usługi Azure stosu | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tworzenia nowej nazwy głównej usługi, który może służyć z kontroli dostępu opartej na rolach w usłudze Azure Resource Manager do zarządzania dostępem do zasobów."
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/17/2017
ms.author: helaw
ms.openlocfilehash: 96d5cdfc28759fd516eab5fd97c6cf444af08cf6
ms.sourcegitcommit: bd0d3ae20773fc87b19dd7f9542f3960211495f9
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/18/2017
---
# <a name="provide-applications-access-to-azure-stack"></a>Zapewnianie dostępu aplikacji do stosu Azure

*Dotyczy: Azure stosu zintegrowanych systemów i Azure stosu Development Kit*

Gdy aplikacja potrzebuje dostępu do wdrażania lub skonfigurować zasoby za pośrednictwem usługi Azure Resource Manager w stosie Azure, można utworzyć nazwy głównej usługi, który jest poświadczenia dla aplikacji.  Następnie można oddelegować uprawnienia niezbędne do tej nazwy głównej usługi.  

Na przykład może być narzędziem do zarządzania konfiguracji korzystającą z usługi Azure Resource Manager w celu spisu zasobów platformy Azure.  W tym scenariuszu można utworzyć nazwy głównej usługi, przyznaj rolę czytelnika do tej nazwy głównej usługi i ograniczyć zarządzania za pomocą narzędzia konfiguracji dostępu tylko do odczytu. 

Nazwy główne usług są preferowane w porównaniu do uruchamiania aplikacji z poświadczeniami użytkownika, ponieważ:

* Można przypisać uprawnienia do podmiotu zabezpieczeń, które są inne niż uprawnień konta usługi. Zazwyczaj te uprawnienia są ograniczone do dokładnie co aplikacja powinna wykonać.
* Nie masz umożliwia zmianę poświadczeń aplikacji Zmień Twoje obowiązki.
* Certyfikat służy do automatyzacji procesu uwierzytelniania podczas wykonywania skryptu instalacji nienadzorowanej.  

## <a name="getting-started"></a>Wprowadzenie

W zależności od tego, jak zostały wdrożone stosu Azure możesz uruchomić tworzenie główną usługi.  W tym dokumencie opisano przez proces tworzenia nazwy głównej usługi dla obu [usługi Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) i [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).  Po utworzeniu nazwy głównej usługi zestaw wspólnych kroków do usług AD FS i usługi Azure Active Directory są używane do [delegować uprawnienia](azure-stack-create-service-principals.md#assign-role-to-service-principal) do roli.     

## <a name="create-service-principal-for-azure-ad"></a>Tworzenie nazwy głównej usługi dla usługi Azure AD

Jeśli została wdrożona przy użyciu usługi Azure AD jako magazynu tożsamości stosu Azure, można utworzyć nazwy główne usług, podobnie jak w przypadku usługi Azure.  W tej sekcji przedstawiono sposób wykonywania kroków za pośrednictwem portalu.  Sprawdź, czy masz [wymagane uprawnienia usługi Azure AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) przed rozpoczęciem.

### <a name="create-service-principal"></a>Tworzenie jednostki usługi
W tej sekcji utworzysz aplikację (nazwy głównej usługi) w usłudze Azure AD, która reprezentuje aplikacji.

1. Zaloguj się do konta platformy Azure za pośrednictwem [portalu Azure](https://portal.azure.com).
2. Wybierz **usługi Azure Active Directory** > **rejestracji aplikacji** > **Dodaj**   
3. Podaj nazwę i adres URL dla aplikacji. Wybierz opcję **aplikacji sieci Web / interfejs API** lub **natywnego** dla typu aplikacji, w którym chcesz utworzyć. Po ustawieniu wartości, wybierz **Utwórz**.

Utworzono nazwy głównej usługi dla aplikacji.

### <a name="get-credentials"></a>Pobieranie poświadczeń
Podczas logowania programowo, można użyć Identyfikatora aplikacji i klucz uwierzytelniania. Aby uzyskać te wartości, wykonaj następujące kroki:

1. Z **rejestracji aplikacji** w usłudze Active Directory, wybierz aplikację.

2. Kopiuj **identyfikator aplikacji** i zapisze go w kodzie aplikacji. Aplikacje w [przykładowe aplikacje](#sample-applications) sekcji odnoszą się do tej wartości jako identyfikator klienta.

     ![Identyfikator klienta](./media/azure-stack-create-service-principal/image12.png)
3. Aby wygenerować klucz uwierzytelniania, wybierz **klucze**.

4. Podaj opis klucza i czas trwania dla klucza. Po zakończeniu wybierz **zapisać**.

Po zapisaniu klucza, wyświetlana jest wartość klucza. Skopiuj tę wartość, ponieważ nie można pobrać klucza później. Musisz podać wartość tego klucza z Identyfikatorem aplikacji do podpisania co aplikacja. Przechowywanie wartości klucza, gdzie aplikacja je pobrać.

![zapisano klucza](./media/azure-stack-create-service-principal/image15.png)


Po wykonaniu tych czynności, przejdź do [przypisywanie roli aplikacji](azure-stack-create-service-principals.md#assign-role-to-service-principal).

## <a name="create-service-principal-for-ad-fs"></a>Tworzenie nazwy głównej usługi dla usług AD FS
Jeśli wdrożono stosu Azure z usługami AD FS, można użyć programu PowerShell do tworzenia nazwy głównej usługi, Przypisz rolę dostępu i zaloguj się z programu PowerShell przy użyciu tej tożsamości.

Skrypt jest uruchamiany z uprzywilejowanego punktu końcowego na maszynie wirtualnej ERCS.


Wymagania:
- Wymagany jest uwierzytelniony.

**Parametry**

Wymagane są następujące informacje jako dane wejściowe dla parametrów automatyzacji:


|Parametr|Opis|Przykład|
|---------|---------|---------|
|Nazwa|Nazwa SPN konta|Moja_aplikacja|
|Właściwość ClientCertificates|Tablica obiektów certyfikatu|X509 certyfikatu|
|ClientRedirectUris<br>(Opcjonalnie)|Identyfikator URI przekierowania aplikacji|         |

**Przykład**

1. Otwórz sesję środowiska Windows PowerShell z podwyższonym poziomem uprawnień i uruchom następujące polecenia:

   > [!NOTE]
   > W tym przykładzie tworzy certyfikat z podpisem własnym. Po uruchomieniu tych poleceń w środowisku produkcyjnym należy używać Get-certyfikatu można pobrać obiektu certyfikatu dla certyfikatu, którego chcesz użyć.

   ```
   $creds = Get-Credential

   $session = New-PSSession -ComputerName <IP Address of ECRS> -ConfigurationName PrivilegedEndpoint -Credential $creds

   $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=testspn2" -KeySpec KeyExchange

   Invoke-Command -Session $session -ScriptBlock { New-GraphApplication -Name 'MyApp' -ClientCertificates $using:cert}

   $session|remove-pssession

   ```

2. Po zakończeniu pracy automatyzacji przedstawia wymagane szczegóły, aby użyć nazwy SPN. 

   Na przykład:

   ```
   ApplicationIdentifier : S-1-5-21-1512385356-3796245103-1243299919-1356
   ClientId              : 3c87e710-9f91-420b-b009-31fa9e430145
   Thumbprint            : 30202C11BE6864437B64CE36C8D988442082A0F1
   ApplicationName       : Azurestack-MyApp-c30febe7-1311-4fd8-9077-3d869db28342
   PSComputerName        : azs-ercs01
   RunspaceId            : a78c76bb-8cae-4db4-a45a-c1420613e01b
   ```
### <a name="assign-a-role"></a>Przypisywanie roli
Po utworzeniu nazwy głównej usługi, należy najpierw [przypisać rolę](azure-stack-create-service-principals.md#assign-role-to-service-principal)

### <a name="sign-in-through-powershell"></a>Zaloguj się za pomocą programu PowerShell
Gdy rola jest przypisywana, można logowania się do stosu Azure przy użyciu nazwy głównej usługi za pomocą następującego polecenia:

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-to-service-principal"></a>Przypisz rolę do nazwy głównej usługi
Aby uzyskać dostęp do zasobów w ramach subskrypcji, należy przypisać aplikacji do roli. Zdecyduj, które roli reprezentuje odpowiednich uprawnień dla aplikacji. Aby dowiedzieć się więcej o dostępnych ról, zobacz [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).

Na poziomie subskrypcji, grupy zasobów lub zasobów można ustawić zakresu. Uprawnienia są dziedziczone na niższe poziomy zakresu. Na przykład dodawanie aplikacji do roli czytnik dla grupy zasobów oznacza, że mogą odczytywać, grupy zasobów i wszystkie zasoby, które zawiera.

1. W portalu Azure stosu przejdź na poziom zakresu, który chcesz przypisać aplikację do. Na przykład, aby przypisać rolę w zakresie subskrypcji, wybierz **subskrypcje**. Zamiast tego możesz określić, grupy zasobów lub zasobu.

2. Umożliwia określonej subskrypcji (grupy zasobów lub zasobów), aby przypisać tę aplikację.

     ![Wybierz subskrypcję do przypisania](./media/azure-stack-create-service-principal/image16.png)

3. Wybierz **(IAM) kontroli dostępu**.

     ![Wybierz dostępu](./media/azure-stack-create-service-principal/image17.png)

4. Wybierz pozycję **Dodaj**.

5. Wybierz rolę, którą chcesz przypisać do aplikacji.

6. Wyszukaj aplikację i zaznacz go.

7. Wybierz **OK** na zakończenie przypisanie roli. Zostanie wyświetlona aplikacja w listy użytkowników przypisanych do roli dla tego zakresu.

Teraz, utworzeniu nazwy głównej usługi i przypisaną rolę, możesz rozpocząć za pomocą tej w aplikacji dostęp do zasobów Azure stosu.  

## <a name="next-steps"></a>Następne kroki

[Dodawanie użytkowników dla usług AD FS](azure-stack-add-users-adfs.md)
[Zarządzaj uprawnieniami użytkowników](azure-stack-manage-permissions.md)