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
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="60bd5-104">Użyj interfejsu wiersza polecenia Azure toocreate zasobów tooaccess głównej usługi</span><span class="sxs-lookup"><span data-stu-id="60bd5-104">Use Azure CLI toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="60bd5-105">Gdy aplikacja lub skrypt, który wymaga tooaccess zasobów, można skonfigurować tożsamości dla aplikacji hello i uwierzytelniania aplikacji hello z własne poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="60bd5-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="60bd5-106">Ta tożsamość jest określany jako nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="60bd5-106">This identity is known as a service principal.</span></span> <span data-ttu-id="60bd5-107">Takie podejście umożliwia:</span><span class="sxs-lookup"><span data-stu-id="60bd5-107">This approach enables you to:</span></span>

* <span data-ttu-id="60bd5-108">Przypisz uprawnienia toohello tożsamości aplikacji, które są inne niż własnych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="60bd5-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="60bd5-109">Zazwyczaj te uprawnienia są ograniczone tooexactly jakie aplikacji hello musi toodo.</span><span class="sxs-lookup"><span data-stu-id="60bd5-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="60bd5-110">Użyj certyfikatu do uwierzytelnienia, podczas wykonywania skryptu instalacji nienadzorowanej.</span><span class="sxs-lookup"><span data-stu-id="60bd5-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="60bd5-111">W tym artykule opisano sposób toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset się toorun aplikacji w ramach własnej poświadczeń i tożsamości.</span><span class="sxs-lookup"><span data-stu-id="60bd5-111">This article shows you how toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset up an application toorun under its own credentials and identity.</span></span> <span data-ttu-id="60bd5-112">Zainstaluj najnowszą wersję hello z [Azure CLI 1.0](../cli-install-nodejs.md) toomake się środowisko odpowiada hello przykłady w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="60bd5-112">Install hello latest version of [Azure CLI 1.0](../cli-install-nodejs.md) toomake sure your environment matches hello examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="60bd5-113">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="60bd5-113">Required permissions</span></span>
<span data-ttu-id="60bd5-114">toocomplete tego tematu, należy posiadać odpowiednie uprawnienia w usłudze Azure Active Directory i Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60bd5-114">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="60bd5-115">W szczególności muszą być stanie toocreate aplikację w hello Azure Active Directory i przypisz rolę tooa główna usługi hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-115">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="60bd5-116">Hello jest czy Twoje konto ma odpowiednie uprawnienia za pośrednictwem portalu hello najprostszym toocheck sposób.</span><span class="sxs-lookup"><span data-stu-id="60bd5-116">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="60bd5-117">Zobacz [Sprawdzanie wymaganego uprawnienia w portalu](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="60bd5-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="60bd5-118">Teraz kontynuować sekcji tooa jednego [hasło](#create-service-principal-with-password) lub [certyfikatu](#create-service-principal-with-certificate) uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="60bd5-118">Now, proceed tooa section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="60bd5-119">Tworzenie nazwy głównej usługi z hasłem</span><span class="sxs-lookup"><span data-stu-id="60bd5-119">Create service principal with password</span></span>
<span data-ttu-id="60bd5-120">W tej sekcji należy wykonać hello kroki toocreate hello aplikacji usługi AD za pomocą hasła i przypisać nazwy głównej usługi toohello hello czytnika roli.</span><span class="sxs-lookup"><span data-stu-id="60bd5-120">In this section, you perform hello steps toocreate hello AD application with a password, and assign hello Reader role toohello service principal.</span></span>

1. <span data-ttu-id="60bd5-121">Zaloguj się na koncie tooyour.</span><span class="sxs-lookup"><span data-stu-id="60bd5-121">Sign in tooyour account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="60bd5-122">toocreate tożsamości aplikacji zawierają hello Nazwa aplikacji hello i hasło, jak pokazano w hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="60bd5-122">toocreate an app identity, provide hello name of hello app and a password, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="60bd5-123">zwracany jest Hello nową usługę podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="60bd5-123">hello new service principal is returned.</span></span> <span data-ttu-id="60bd5-124">Hello identyfikator obiektu jest potrzebne podczas udzielania uprawnień.</span><span class="sxs-lookup"><span data-stu-id="60bd5-124">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="60bd5-125">identyfikator guid Hello na liście z hello główne nazwy usług jest potrzebne podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="60bd5-125">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="60bd5-126">Ten identyfikator guid jest hello tę samą wartość jak identyfikator aplikacji hello. W hello przykładowych aplikacji, ta wartość jest hello tooas określonego `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="60bd5-126">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello `Client ID`.</span></span> 
     
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

3. <span data-ttu-id="60bd5-127">Przyznaj uprawnienia hello usługa podmiotu zabezpieczeń w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="60bd5-127">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="60bd5-128">W tym przykładzie możesz dodać rolę czytelnika toohello główna usługi hello, co powoduje przyznanie uprawnień tooread wszystkich zasobów w subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-128">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="60bd5-129">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="60bd5-129">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="60bd5-130">Dla parametru objectid hello Podaj identyfikator obiektu, który został użyty podczas tworzenia aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-130">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="60bd5-131">Przed uruchomieniem tego polecenia, musisz zezwolić na chwilę, aż hello nowej usługi głównej toopropagate w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60bd5-131">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="60bd5-132">Po uruchomieniu tych poleceń ręcznie, zwykle wystarczająco dużo czasu upłynął między zadaniami.</span><span class="sxs-lookup"><span data-stu-id="60bd5-132">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="60bd5-133">W skrypcie, należy dodać krok toosleep między hello poleceń (takich jak `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="60bd5-133">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="60bd5-134">Jeśli zostanie wyświetlony błąd określania hello główny nie istnieje w katalogu hello, ponownie uruchom polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-134">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="60bd5-135">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="60bd5-135">That's it!</span></span> <span data-ttu-id="60bd5-136">Twojej aplikacji usługi AD i nazwę główną usługi są skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="60bd5-136">Your AD application and service principal are set up.</span></span> <span data-ttu-id="60bd5-137">Witaj następnej części pokazano, jak toolog się przy użyciu hello poświadczeń za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="60bd5-137">hello next section shows you how toolog in with hello credential through Azure CLI.</span></span> <span data-ttu-id="60bd5-138">Jeśli chcesz toouse hello poświadczeń w kodzie aplikacji, nie trzeba toocontinue z tego tematu.</span><span class="sxs-lookup"><span data-stu-id="60bd5-138">If you want toouse hello credential in your code application, you do not need toocontinue with this topic.</span></span> <span data-ttu-id="60bd5-139">Można przechodzić toohello [przykładowe aplikacje](#sample-applications) przykłady logowania się za pomocą identyfikatora aplikacji id oraz hasła.</span><span class="sxs-lookup"><span data-stu-id="60bd5-139">You can jump toohello [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="60bd5-140">Podaj poświadczenia, za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="60bd5-140">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="60bd5-141">Teraz należy toolog w jako operacji tooperform aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-141">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="60bd5-142">Gdy zalogujesz się jako nazwy głównej usługi, potrzebny jest identyfikator dzierżawcy hello tooprovide hello katalogu dla aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="60bd5-142">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="60bd5-143">Dzierżawa jest wystąpieniem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60bd5-143">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="60bd5-144">Identyfikator dzierżawy hello tooretrieve uwierzytelnionym subskrypcji, użyj:</span><span class="sxs-lookup"><span data-stu-id="60bd5-144">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="60bd5-145">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="60bd5-145">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="60bd5-146">Identyfikator dzierżawy hello tooget inną subskrypcję, należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="60bd5-146">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="60bd5-147">Jeśli potrzebujesz tooretrieve powitania klienta identyfikator toouse rejestrowanie użyć:</span><span class="sxs-lookup"><span data-stu-id="60bd5-147">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="60bd5-148">toouse wartość Hello rejestrowanie jest guid hello na liście hello głównych nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="60bd5-148">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
   
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
3. <span data-ttu-id="60bd5-149">Zaloguj się jako nazwy głównej usługi hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-149">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="60bd5-150">Zostanie wyświetlony monit o hasło hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-150">You are prompted for hello password.</span></span> <span data-ttu-id="60bd5-151">Podaj hasło hello, określone podczas tworzenia aplikacji hello AD.</span><span class="sxs-lookup"><span data-stu-id="60bd5-151">Provide hello password you specified when creating hello AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="60bd5-152">Obecnie użytkownik jest uwierzytelniony jako hello nazwy głównej usługi dla nazwy głównej usługi hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="60bd5-152">You are now authenticated as hello service principal for hello service principal that you created.</span></span>

<span data-ttu-id="60bd5-153">Alternatywnie można wywołać operacji REST z hello toolog wiersza polecenia w.</span><span class="sxs-lookup"><span data-stu-id="60bd5-153">Alternatively, you can invoke REST operations from hello command line toolog in.</span></span> <span data-ttu-id="60bd5-154">Z odpowiedzi uwierzytelniania hello można pobrać tokenu dostępu hello do użytku z innymi operacjami.</span><span class="sxs-lookup"><span data-stu-id="60bd5-154">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="60bd5-155">Na przykład pobierania tokenu dostępu hello przez wywołanie operacji REST, zobacz [generowania tokenu dostępu](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="60bd5-155">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="60bd5-156">Tworzenie nazwy głównej usługi o certyfikat</span><span class="sxs-lookup"><span data-stu-id="60bd5-156">Create service principal with certificate</span></span>
<span data-ttu-id="60bd5-157">W tej sekcji należy wykonać kroki hello do:</span><span class="sxs-lookup"><span data-stu-id="60bd5-157">In this section, you perform hello steps to:</span></span>

* <span data-ttu-id="60bd5-158">Utwórz certyfikat z podpisem własnym</span><span class="sxs-lookup"><span data-stu-id="60bd5-158">create a self-signed certificate</span></span>
* <span data-ttu-id="60bd5-159">Tworzenie hello aplikacji usługi AD przy użyciu certyfikatu hello i hello nazwy głównej usługi</span><span class="sxs-lookup"><span data-stu-id="60bd5-159">create hello AD application with hello certificate, and hello service principal</span></span>
* <span data-ttu-id="60bd5-160">Przypisz nazwę główną usługi toohello hello czytnika roli</span><span class="sxs-lookup"><span data-stu-id="60bd5-160">assign hello Reader role toohello service principal</span></span>

<span data-ttu-id="60bd5-161">toocomplete tych kroków, musi mieć [OpenSSL](http://www.openssl.org/) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="60bd5-161">toocomplete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="60bd5-162">Tworzenie certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="60bd5-162">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="60bd5-163">Witaj poprzedzających krok utworzyć dwa pliki - privkey.pem i cert.pem.</span><span class="sxs-lookup"><span data-stu-id="60bd5-163">hello preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="60bd5-164">Łączenie hello klucze publiczne i prywatne w jednym pliku.</span><span class="sxs-lookup"><span data-stu-id="60bd5-164">Combine hello public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="60bd5-165">Otwórz hello **examplecert.pem** pliku i poszukaj hello długo sekwencja znaków między **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---**.</span><span class="sxs-lookup"><span data-stu-id="60bd5-165">Open hello **examplecert.pem** file and look for hello long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="60bd5-166">Skopiuj dane certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-166">Copy hello certificate data.</span></span> <span data-ttu-id="60bd5-167">Te dane należy przekazać jako parametru podczas tworzenia hello nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="60bd5-167">You pass this data as a parameter when creating hello service principal.</span></span>

4. <span data-ttu-id="60bd5-168">Zaloguj się na koncie tooyour.</span><span class="sxs-lookup"><span data-stu-id="60bd5-168">Sign in tooyour account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="60bd5-169">nazwy głównej usługi hello toocreate, podaj nazwę hello hello aplikacji i danych certyfikatu hello, jak pokazano w hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="60bd5-169">toocreate hello service principal, provide hello name of hello app and hello certificate data, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="60bd5-170">zwracany jest Hello nową usługę podmiotu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="60bd5-170">hello new service principal is returned.</span></span> <span data-ttu-id="60bd5-171">Hello identyfikator obiektu jest potrzebne podczas udzielania uprawnień.</span><span class="sxs-lookup"><span data-stu-id="60bd5-171">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="60bd5-172">identyfikator guid Hello na liście z hello główne nazwy usług jest potrzebne podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="60bd5-172">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="60bd5-173">Ten identyfikator guid jest hello tę samą wartość jak identyfikator aplikacji hello. W hello przykładowych aplikacji ta wartość jest hello tooas określony identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="60bd5-173">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello Client ID.</span></span> 
     
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
6. <span data-ttu-id="60bd5-174">Przyznaj uprawnienia hello usługa podmiotu zabezpieczeń w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="60bd5-174">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="60bd5-175">W tym przykładzie możesz dodać rolę czytelnika toohello główna usługi hello, co powoduje przyznanie uprawnień tooread wszystkich zasobów w subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-175">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="60bd5-176">Dla innych ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="60bd5-176">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="60bd5-177">Dla parametru objectid hello Podaj identyfikator obiektu, który został użyty podczas tworzenia aplikacji hello hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-177">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="60bd5-178">Przed uruchomieniem tego polecenia, musisz zezwolić na chwilę, aż hello nowej usługi głównej toopropagate w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60bd5-178">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="60bd5-179">Po uruchomieniu tych poleceń ręcznie, zwykle wystarczająco dużo czasu upłynął między zadaniami.</span><span class="sxs-lookup"><span data-stu-id="60bd5-179">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="60bd5-180">W skrypcie, należy dodać krok toosleep między hello poleceń (takich jak `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="60bd5-180">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="60bd5-181">Jeśli zostanie wyświetlony błąd określania hello główny nie istnieje w katalogu hello, ponownie uruchom polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-181">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="60bd5-182">Podaj certyfikat przy użyciu zautomatyzowanego skryptu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="60bd5-182">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="60bd5-183">Teraz należy toolog w jako operacji tooperform aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-183">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="60bd5-184">Gdy zalogujesz się jako nazwy głównej usługi, potrzebny jest identyfikator dzierżawcy hello tooprovide hello katalogu dla aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="60bd5-184">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="60bd5-185">Dzierżawa jest wystąpieniem usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60bd5-185">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="60bd5-186">Identyfikator dzierżawy hello tooretrieve uwierzytelnionym subskrypcji, użyj:</span><span class="sxs-lookup"><span data-stu-id="60bd5-186">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="60bd5-187">Polecenie to zwraca:</span><span class="sxs-lookup"><span data-stu-id="60bd5-187">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="60bd5-188">Identyfikator dzierżawy hello tooget inną subskrypcję, należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="60bd5-188">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="60bd5-189">tooretrieve hello odcisk palca certyfikatu i usuń zbędne znaki, użyj:</span><span class="sxs-lookup"><span data-stu-id="60bd5-189">tooretrieve hello certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="60bd5-190">Która zwróci wartość odcisku palca są podobne do:</span><span class="sxs-lookup"><span data-stu-id="60bd5-190">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="60bd5-191">Jeśli potrzebujesz tooretrieve powitania klienta identyfikator toouse rejestrowanie użyć:</span><span class="sxs-lookup"><span data-stu-id="60bd5-191">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="60bd5-192">toouse wartość Hello rejestrowanie jest guid hello na liście hello głównych nazw usługi.</span><span class="sxs-lookup"><span data-stu-id="60bd5-192">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
     
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
4. <span data-ttu-id="60bd5-193">Zaloguj się jako nazwy głównej usługi hello.</span><span class="sxs-lookup"><span data-stu-id="60bd5-193">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="60bd5-194">Obecnie użytkownik jest uwierzytelniony jako nazwy głównej usługi hello na powitania utworzona aplikacja usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="60bd5-194">You are now authenticated as hello service principal for hello Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="60bd5-195">Zmiana poświadczeń</span><span class="sxs-lookup"><span data-stu-id="60bd5-195">Change credentials</span></span>

<span data-ttu-id="60bd5-196">Użyj poświadczeń hello toochange dla aplikacji usługi AD, albo z powodu naruszenia zabezpieczeń lub wygaśnięcia poświadczeń, `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="60bd5-196">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="60bd5-197">toochange hasła, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="60bd5-197">toochange a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="60bd5-198">toochange wartość certyfikatu, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="60bd5-198">toochange a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="60bd5-199">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="60bd5-199">Debug</span></span>

<span data-ttu-id="60bd5-200">Mogą wystąpić następujące błędy podczas tworzenia nazwy głównej usługi hello:</span><span class="sxs-lookup"><span data-stu-id="60bd5-200">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="60bd5-201">**"Authentication_Unauthorized"** lub **"subskrypcji nie znaleziono w kontekście hello".**</span><span class="sxs-lookup"><span data-stu-id="60bd5-201">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="60bd5-202">— Został wyświetlony ten błąd, gdy Twoje konto nie ma hello [wymagane uprawnienia](#required-permissions) na hello Azure Active Directory tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="60bd5-202">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="60bd5-203">Zwykle zostanie wyświetlony ten błąd, gdy tylko Administrator użytkowników w usłudze Azure Active Directory można zarejestrować aplikacji, a konto użytkownika nie jest administratorem. Poproś tooeither Twojego administratora przypisać możesz tooan rolę administratora lub tooenable użytkowników tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="60bd5-203">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="60bd5-204">Twoje konto **"nie ma autoryzacji tooperform akcji"Microsoft.Authorization/roleAssignments/write"w zakresie"/subscriptions/ {guid}"." ** — Zostanie wyświetlony ten błąd, gdy Twoje konto nie ma wystarczających uprawnień tooassign tożsamości tooan roli.</span><span class="sxs-lookup"><span data-stu-id="60bd5-204">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="60bd5-205">Skontaktuj się z tooadd administratora subskrypcji możesz tooUser dostępu do roli administratora.</span><span class="sxs-lookup"><span data-stu-id="60bd5-205">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="60bd5-206">Przykładowe aplikacje</span><span class="sxs-lookup"><span data-stu-id="60bd5-206">Sample applications</span></span>
<span data-ttu-id="60bd5-207">Aby uzyskać informacje o zalogowanie się jako aplikacji hello za pomocą różnych platform zobacz:</span><span class="sxs-lookup"><span data-stu-id="60bd5-207">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="60bd5-208">.NET</span><span class="sxs-lookup"><span data-stu-id="60bd5-208">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="60bd5-209">Java</span><span class="sxs-lookup"><span data-stu-id="60bd5-209">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="60bd5-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="60bd5-210">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="60bd5-211">Python</span><span class="sxs-lookup"><span data-stu-id="60bd5-211">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="60bd5-212">Ruby</span><span class="sxs-lookup"><span data-stu-id="60bd5-212">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="60bd5-213">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60bd5-213">Next steps</span></span>
* <span data-ttu-id="60bd5-214">Aby uzyskać szczegółowe instrukcje dotyczące integrowania aplikacji na platformie Azure do zarządzania zasobami, zobacz [tooauthorization przewodnik dewelopera programu z interfejsu API usługi Azure Resource Manager hello](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="60bd5-214">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="60bd5-215">Zobacz więcej informacji o używaniu certyfikatów i interfejsu wiersza polecenia Azure, tooget [uwierzytelniania opartego na certyfikatach z podmiotami zabezpieczeń usługi Azure z wiersza polecenia systemu Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="60bd5-215">tooget more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="60bd5-216">Aby uzyskać listę dostępnych akcji, które można udzielić lub odmówić toousers, zobacz [operacji dostawcy zasobów usługi Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="60bd5-216">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
