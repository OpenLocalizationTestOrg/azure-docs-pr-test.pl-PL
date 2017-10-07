---
title: "tożsamość aaaCreate dla aplikacji platformy Azure za pomocą wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse interfejsu wiersza polecenia Azure toocreate aplikację usługi Azure Active Directory i nazwy głównej usługi i przyznać dostęp do tooresources za pomocą dostępu opartej na rolach kontroli. Widoczny jest sposób tooauthenticate aplikacji za pomocą hasła lub certyfikatu."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>Użyj interfejsu wiersza polecenia Azure toocreate zasobów tooaccess głównej usługi

Gdy aplikacja lub skrypt, który wymaga tooaccess zasobów, można skonfigurować tożsamości dla aplikacji hello i uwierzytelniania aplikacji hello z własne poświadczenia. Ta tożsamość jest określany jako nazwy głównej usługi. Takie podejście umożliwia:

* Przypisz uprawnienia toohello tożsamości aplikacji, które są inne niż własnych uprawnień. Zazwyczaj te uprawnienia są ograniczone tooexactly jakie aplikacji hello musi toodo.
* Użyj certyfikatu do uwierzytelnienia, podczas wykonywania skryptu instalacji nienadzorowanej.

W tym artykule opisano sposób toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset się toorun aplikacji w ramach własnej poświadczeń i tożsamości. Zainstaluj najnowszą wersję hello z [Azure CLI 1.0](../cli-install-nodejs.md) toomake się środowisko odpowiada hello przykłady w tym artykule.

## <a name="required-permissions"></a>Wymagane uprawnienia
toocomplete tego tematu, należy posiadać odpowiednie uprawnienia w usłudze Azure Active Directory i Twojej subskrypcji platformy Azure. W szczególności muszą być stanie toocreate aplikację w hello Azure Active Directory i przypisz rolę tooa główna usługi hello. 

Hello jest czy Twoje konto ma odpowiednie uprawnienia za pośrednictwem portalu hello najprostszym toocheck sposób. Zobacz [Sprawdzanie wymaganego uprawnienia w portalu](resource-group-create-service-principal-portal.md#required-permissions).

Teraz kontynuować sekcji tooa jednego [hasło](#create-service-principal-with-password) lub [certyfikatu](#create-service-principal-with-certificate) uwierzytelniania.

## <a name="create-service-principal-with-password"></a>Tworzenie nazwy głównej usługi z hasłem
W tej sekcji należy wykonać hello kroki toocreate hello aplikacji usługi AD za pomocą hasła i przypisać nazwy głównej usługi toohello hello czytnika roli.

1. Zaloguj się na koncie tooyour.
   
   ```azurecli
   azure login
   ```
2. toocreate tożsamości aplikacji zawierają hello Nazwa aplikacji hello i hasło, jak pokazano w hello następujące polecenie:
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   zwracany jest Hello nową usługę podmiotu zabezpieczeń. Hello identyfikator obiektu jest potrzebne podczas udzielania uprawnień. identyfikator guid Hello na liście z hello główne nazwy usług jest potrzebne podczas logowania. Ten identyfikator guid jest hello tę samą wartość jak identyfikator aplikacji hello. W hello przykładowych aplikacji, ta wartość jest hello tooas określonego `Client ID`. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. Przyznaj uprawnienia hello usługa podmiotu zabezpieczeń w ramach subskrypcji. W tym przykładzie możesz dodać rolę czytelnika toohello główna usługi hello, co powoduje przyznanie uprawnień tooread wszystkich zasobów w subskrypcji hello. Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md). Dla parametru objectid hello Podaj identyfikator obiektu, który został użyty podczas tworzenia aplikacji hello hello. Przed uruchomieniem tego polecenia, musisz zezwolić na chwilę, aż hello nowej usługi głównej toopropagate w usłudze Azure Active Directory. Po uruchomieniu tych poleceń ręcznie, zwykle wystarczająco dużo czasu upłynął między zadaniami. W skrypcie, należy dodać krok toosleep między hello poleceń (takich jak `sleep 15`). Jeśli zostanie wyświetlony błąd określania hello główny nie istnieje w katalogu hello, ponownie uruchom polecenie hello.
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
Gotowe. Twojej aplikacji usługi AD i nazwę główną usługi są skonfigurowane. Witaj następnej części pokazano, jak toolog się przy użyciu hello poświadczeń za pomocą wiersza polecenia platformy Azure. Jeśli chcesz toouse hello poświadczeń w kodzie aplikacji, nie trzeba toocontinue z tego tematu. Można przechodzić toohello [przykładowe aplikacje](#sample-applications) przykłady logowania się za pomocą identyfikatora aplikacji id oraz hasła. 

### <a name="provide-credentials-through-azure-cli"></a>Podaj poświadczenia, za pomocą wiersza polecenia platformy Azure
Teraz należy toolog w jako operacji tooperform aplikacji hello.

1. Gdy zalogujesz się jako nazwy głównej usługi, potrzebny jest identyfikator dzierżawcy hello tooprovide hello katalogu dla aplikacji usługi AD. Dzierżawa jest wystąpieniem usługi Azure Active Directory. Identyfikator dzierżawy hello tooretrieve uwierzytelnionym subskrypcji, użyj:
   
   ```azurecli
   azure account show
   ```
   
   Polecenie to zwraca:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     Identyfikator dzierżawy hello tooget inną subskrypcję, należy użyć hello następujące polecenie:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. Jeśli potrzebujesz tooretrieve powitania klienta identyfikator toouse rejestrowanie użyć:
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     toouse wartość Hello rejestrowanie jest guid hello na liście hello głównych nazw usługi.
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. Zaloguj się jako nazwy głównej usługi hello.
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    Zostanie wyświetlony monit o hasło hello. Podaj hasło hello, określone podczas tworzenia aplikacji hello AD.
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

Obecnie użytkownik jest uwierzytelniony jako hello nazwy głównej usługi dla nazwy głównej usługi hello utworzony.

Alternatywnie można wywołać operacji REST z hello toolog wiersza polecenia w. Z odpowiedzi uwierzytelniania hello można pobrać tokenu dostępu hello do użytku z innymi operacjami. Na przykład pobierania tokenu dostępu hello przez wywołanie operacji REST, zobacz [generowania tokenu dostępu](resource-manager-rest-api.md#generating-an-access-token).

## <a name="create-service-principal-with-certificate"></a>Tworzenie nazwy głównej usługi o certyfikat
W tej sekcji należy wykonać kroki hello do:

* Utwórz certyfikat z podpisem własnym
* Tworzenie hello aplikacji usługi AD przy użyciu certyfikatu hello i hello nazwy głównej usługi
* Przypisz nazwę główną usługi toohello hello czytnika roli

toocomplete tych kroków, musi mieć [OpenSSL](http://www.openssl.org/) zainstalowane.

1. Tworzenie certyfikatu z podpisem własnym.
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. Witaj poprzedzających krok utworzyć dwa pliki - privkey.pem i cert.pem. Łączenie hello klucze publiczne i prywatne w jednym pliku.

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. Otwórz hello **examplecert.pem** pliku i poszukaj hello długo sekwencja znaków między **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---**. Skopiuj dane certyfikatu hello. Te dane należy przekazać jako parametru podczas tworzenia hello nazwy głównej usługi.

4. Zaloguj się na koncie tooyour.

   ```azurecli
   azure login
   ```
5. nazwy głównej usługi hello toocreate, podaj nazwę hello hello aplikacji i danych certyfikatu hello, jak pokazano w hello następujące polecenie:
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   zwracany jest Hello nową usługę podmiotu zabezpieczeń. Hello identyfikator obiektu jest potrzebne podczas udzielania uprawnień. identyfikator guid Hello na liście z hello główne nazwy usług jest potrzebne podczas logowania. Ten identyfikator guid jest hello tę samą wartość jak identyfikator aplikacji hello. W hello przykładowych aplikacji ta wartość jest hello tooas określony identyfikator klienta. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. Przyznaj uprawnienia hello usługa podmiotu zabezpieczeń w ramach subskrypcji. W tym przykładzie możesz dodać rolę czytelnika toohello główna usługi hello, co powoduje przyznanie uprawnień tooread wszystkich zasobów w subskrypcji hello. Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md). Dla parametru objectid hello Podaj identyfikator obiektu, który został użyty podczas tworzenia aplikacji hello hello. Przed uruchomieniem tego polecenia, musisz zezwolić na chwilę, aż hello nowej usługi głównej toopropagate w usłudze Azure Active Directory. Po uruchomieniu tych poleceń ręcznie, zwykle wystarczająco dużo czasu upłynął między zadaniami. W skrypcie, należy dodać krok toosleep między hello poleceń (takich jak `sleep 15`). Jeśli zostanie wyświetlony błąd określania hello główny nie istnieje w katalogu hello, ponownie uruchom polecenie hello.
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>Podaj certyfikat przy użyciu zautomatyzowanego skryptu wiersza polecenia platformy Azure
Teraz należy toolog w jako operacji tooperform aplikacji hello.

1. Gdy zalogujesz się jako nazwy głównej usługi, potrzebny jest identyfikator dzierżawcy hello tooprovide hello katalogu dla aplikacji usługi AD. Dzierżawa jest wystąpieniem usługi Azure Active Directory. Identyfikator dzierżawy hello tooretrieve uwierzytelnionym subskrypcji, użyj:
   
   ```azurecli
   azure account show
   ```
   
   Polecenie to zwraca:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   Identyfikator dzierżawy hello tooget inną subskrypcję, należy użyć hello następujące polecenie:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve hello odcisk palca certyfikatu i usuń zbędne znaki, użyj:
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   Która zwróci wartość odcisku palca są podobne do:
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. Jeśli potrzebujesz tooretrieve powitania klienta identyfikator toouse rejestrowanie użyć:
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   toouse wartość Hello rejestrowanie jest guid hello na liście hello głównych nazw usługi.
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. Zaloguj się jako nazwy głównej usługi hello.
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

Obecnie użytkownik jest uwierzytelniony jako nazwy głównej usługi hello na powitania utworzona aplikacja usługi Azure Active Directory.

## <a name="change-credentials"></a>Zmiana poświadczeń

Użyj poświadczeń hello toochange dla aplikacji usługi AD, albo z powodu naruszenia zabezpieczeń lub wygaśnięcia poświadczeń, `azure ad app set`.

toochange hasła, należy użyć:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

toochange wartość certyfikatu, należy użyć:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>Debugowanie

Mogą wystąpić następujące błędy podczas tworzenia nazwy głównej usługi hello:

* **"Authentication_Unauthorized"** lub **"subskrypcji nie znaleziono w kontekście hello".** — Został wyświetlony ten błąd, gdy Twoje konto nie ma hello [wymagane uprawnienia](#required-permissions) na hello Azure Active Directory tooregister aplikacji. Zwykle zostanie wyświetlony ten błąd, gdy tylko Administrator użytkowników w usłudze Azure Active Directory można zarejestrować aplikacji, a konto użytkownika nie jest administratorem. Poproś tooeither Twojego administratora przypisać możesz tooan rolę administratora lub tooenable użytkowników tooregister aplikacji.

* Twoje konto **"nie ma autoryzacji tooperform akcji"Microsoft.Authorization/roleAssignments/write"w zakresie"/subscriptions/ {guid}"." ** — Zostanie wyświetlony ten błąd, gdy Twoje konto nie ma wystarczających uprawnień tooassign tożsamości tooan roli. Skontaktuj się z tooadd administratora subskrypcji możesz tooUser dostępu do roli administratora.

## <a name="sample-applications"></a>Przykładowe aplikacje
Aby uzyskać informacje o zalogowanie się jako aplikacji hello za pomocą różnych platform zobacz:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać szczegółowe instrukcje dotyczące integrowania aplikacji na platformie Azure do zarządzania zasobami, zobacz [tooauthorization przewodnik dewelopera programu z interfejsu API usługi Azure Resource Manager hello](resource-manager-api-authentication.md).
* Zobacz więcej informacji o używaniu certyfikatów i interfejsu wiersza polecenia Azure, tooget [uwierzytelniania opartego na certyfikatach z podmiotami zabezpieczeń usługi Azure z wiersza polecenia systemu Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx). 
* Aby uzyskać listę dostępnych akcji, które można udzielić lub odmówić toousers, zobacz [operacji dostawcy zasobów usługi Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).
