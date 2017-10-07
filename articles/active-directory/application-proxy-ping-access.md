---
title: "uwierzytelnianie oparte na aaaHeader z PingAccess dla serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Publikowania aplikacji za pomocą PingAccess i serwera Proxy aplikacji toosupport nagłówek uwierzytelniania."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a><span data-ttu-id="a926a-103">Nagłówek uwierzytelniania dla logowania jednokrotnego z serwera Proxy aplikacji i PingAccess</span><span class="sxs-lookup"><span data-stu-id="a926a-103">Header-based authentication for single sign-on with Application Proxy and PingAccess</span></span>

<span data-ttu-id="a926a-104">Azure Active Directory serwera Proxy aplikacji i PingAccess ma współpracę ze sobą tooprovide usługi Azure Active Directory klientom dostępu tooeven więcej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a926a-104">Azure Active Directory Application Proxy and PingAccess have partnered together tooprovide Azure Active Directory customers with access tooeven more applications.</span></span> <span data-ttu-id="a926a-105">PingAccess rozszerza hello [istniejący serwer Proxy aplikacji ofert](active-directory-application-proxy-get-started.md) tooinclude tooapplications dostępu rejestracji jednokrotnej, który nagłówków jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a926a-105">PingAccess expands hello [existing Application Proxy offerings](active-directory-application-proxy-get-started.md) tooinclude single sign-on access tooapplications that use headers for authentication.</span></span>

## <a name="what-is-pingaccess-for-azure-ad"></a><span data-ttu-id="a926a-106">Co to jest PingAccess dla usługi Azure AD?</span><span class="sxs-lookup"><span data-stu-id="a926a-106">What is PingAccess for Azure AD?</span></span>

<span data-ttu-id="a926a-107">PingAccess dla usługi Azure Active Directory jest oferowany PingAccess umożliwiającą toogive użytkowników dostęp i pojedynczego logowania jednokrotnego tooapplications który nagłówków jest używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a926a-107">PingAccess for Azure Active Directory is an offering of PingAccess that enables you toogive users access and single sign-on tooapplications that use headers for authentication.</span></span> <span data-ttu-id="a926a-108">Serwer Proxy aplikacji traktuje te aplikacje, takie jak każdy inny przy użyciu usługi Azure AD tooauthenticate dostępu, a następnie przekazywanie ruchu za pośrednictwem usługi łącznika hello.</span><span class="sxs-lookup"><span data-stu-id="a926a-108">Application Proxy treats these apps like any other, using Azure AD tooauthenticate access and then passing traffic through hello connector service.</span></span> <span data-ttu-id="a926a-109">PingAccess znajduje się na początku aplikacji hello i tłumaczy hello token dostępu z usługi Azure AD na nagłówka, dzięki czemu aplikacja hello odbiera hello uwierzytelniania w formacie hello, który można odczytać.</span><span class="sxs-lookup"><span data-stu-id="a926a-109">PingAccess sits in front of hello apps and translates hello access token from Azure AD into a header so that hello application receives hello authentication in hello format it can read.</span></span>

<span data-ttu-id="a926a-110">Użytkownicy nie będą Zwróć uwagę, inne po zalogowaniu toouse aplikacji firmowych.</span><span class="sxs-lookup"><span data-stu-id="a926a-110">Your users won’t notice anything different when they sign in toouse your corporate apps.</span></span> <span data-ttu-id="a926a-111">Wciąż pracować z dowolnego miejsca na dowolnym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="a926a-111">They can still work from anywhere on any device.</span></span> 

<span data-ttu-id="a926a-112">Ponieważ łączniki serwera Proxy aplikacji hello skierować ruch zdalnego tooall aplikacji niezależnie od ich typ uwierzytelniania, będziesz nadal saldo tooload automatycznie, jak również.</span><span class="sxs-lookup"><span data-stu-id="a926a-112">Since hello Application Proxy connectors direct remote traffic tooall apps regardless of their authentication type, they’ll continue tooload balance automatically, as well.</span></span>

## <a name="how-do-i-get-access"></a><span data-ttu-id="a926a-113">Jak uzyskać dostęp?</span><span class="sxs-lookup"><span data-stu-id="a926a-113">How do I get access?</span></span>

<span data-ttu-id="a926a-114">Ponieważ ten scenariusz jest dostępna za pośrednictwem usługi Azure Active Directory i PingAccess, potrzebnych licencji dla obu usług.</span><span class="sxs-lookup"><span data-stu-id="a926a-114">Since this scenario is offered through a partnership between Azure Active Directory and PingAccess, you need licenses for both services.</span></span> <span data-ttu-id="a926a-115">Jednak subskrypcje usługi Azure Active Directory Premium obejmują podstawowe licencji PingAccess, która obejmuje zapasowe too20 aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a926a-115">However, Azure Active Directory Premium subscriptions include a basic PingAccess license that covers up too20 applications.</span></span> <span data-ttu-id="a926a-116">Jeśli potrzebujesz toopublish więcej niż 20 aplikacji nagłówka, można nabyć od PingAccess dodatkowych licencji.</span><span class="sxs-lookup"><span data-stu-id="a926a-116">If you need toopublish more than 20 header-based applications, you can purchase an additional license from PingAccess.</span></span> 

<span data-ttu-id="a926a-117">Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="a926a-117">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="publish-your-application-in-azure"></a><span data-ttu-id="a926a-118">Publikowanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a926a-118">Publish your application in Azure</span></span>

<span data-ttu-id="a926a-119">Ten artykuł jest przeznaczony dla osób, które są publikowania aplikacji za pomocą tego scenariusza powitania po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="a926a-119">This article is intended for people who are publishing an app with this scenario for hello first time.</span></span> <span data-ttu-id="a926a-120">Go przedstawiono sposób tooget uruchamiania z aplikacji i PingAccess, oprócz toohello kroki publikowania.</span><span class="sxs-lookup"><span data-stu-id="a926a-120">It walks through how tooget started with both Application and PingAccess, in addition toohello publishing steps.</span></span> <span data-ttu-id="a926a-121">Jeśli skonfigurowano już obie usługi, ale odświeżacz na powitania publikowania kroki, możesz pominąć hello instalacja łącznika i przenieść na zbyt[dodać tooAzure Twojej aplikacji usługi Active Directory z serwera Proxy aplikacji](#add-your-app-to-Azure-AD-with-Application-Proxy).</span><span class="sxs-lookup"><span data-stu-id="a926a-121">If you’ve already configured both services but want a refresher on hello publishing steps, you can skip hello connector installation and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-Azure-AD-with-Application-Proxy).</span></span>

>[!NOTE]
><span data-ttu-id="a926a-122">Ponieważ ten scenariusz jest powiązanie między usługą Azure AD i PingAccess, niektóre instrukcje hello istnieją na powitania Ping tożsamości witryny.</span><span class="sxs-lookup"><span data-stu-id="a926a-122">Since this scenario is a partnership between Azure AD and PingAccess, some of hello instructions exist on hello Ping Identity site.</span></span>

### <a name="install-an-application-proxy-connector"></a><span data-ttu-id="a926a-123">Instalowanie łącznika serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a926a-123">Install an Application Proxy connector</span></span>

<span data-ttu-id="a926a-124">Jeśli już ma włączony serwer Proxy aplikacji, a ma zainstalowany łącznik, możesz pominąć tę sekcję i przenieść na zbyt[dodać tooAzure Twojej aplikacji usługi Active Directory z serwera Proxy aplikacji](#add-your-app-to-azure-ad-with-application-proxy).</span><span class="sxs-lookup"><span data-stu-id="a926a-124">If you already have Application Proxy enabled, and have a connector installed, you can skip this section and move on too[Add your app tooAzure AD with Application Proxy](#add-your-app-to-azure-ad-with-application-proxy).</span></span>

<span data-ttu-id="a926a-125">Łącznik serwera Proxy aplikacji Hello jest Windows Server usługi, który kieruje ruch hello z tooyour Twojego pracowników zdalnych opublikowane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="a926a-125">hello Application Proxy connector is a Windows Server service that directs hello traffic from your remote employees tooyour published apps.</span></span> <span data-ttu-id="a926a-126">Aby uzyskać szczegółowe instrukcje dotyczące instalacji, zobacz [Włączanie serwera Proxy aplikacji w portalu Azure hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="a926a-126">For more detailed installation instructions, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

1. <span data-ttu-id="a926a-127">Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator globalny.</span><span class="sxs-lookup"><span data-stu-id="a926a-127">Sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="a926a-128">Wybierz **usługi Azure Active Directory** > **serwera proxy aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a926a-128">Select **Azure Active Directory** > **Application proxy**.</span></span>
3. <span data-ttu-id="a926a-129">Wybierz **Pobierz łącznik** pobieranie łącznika serwera Proxy aplikacji hello toostart.</span><span class="sxs-lookup"><span data-stu-id="a926a-129">Select **Download Connector** toostart hello Application Proxy connector download.</span></span> <span data-ttu-id="a926a-130">Wykonaj instrukcje dotyczące instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="a926a-130">Follow hello installation instructions.</span></span>

   ![Włącz serwer Proxy aplikacji i Pobierz łącznik hello](./media/application-proxy-ping-access/install-connector.png)

4. <span data-ttu-id="a926a-132">Pobieranie łącznika hello automatycznie należy włączyć serwer Proxy aplikacji dla katalogu, ale jeśli nie możesz wybrać **Włączanie serwera Proxy aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a926a-132">Downloading hello connector should automatically enable Application Proxy for your directory, but if not you can select **Enable Application Proxy**.</span></span>


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a><span data-ttu-id="a926a-133">Dodaj użytkownika tooAzure aplikacji usługi Active Directory z serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a926a-133">Add your app tooAzure AD with Application Proxy</span></span>

<span data-ttu-id="a926a-134">Istnieją dwie akcje muszą tootake w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a926a-134">There are two actions you need tootake in hello Azure portal.</span></span> <span data-ttu-id="a926a-135">Najpierw należy toopublish aplikacji przy użyciu serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a926a-135">First, you need toopublish your application with Application Proxy.</span></span> <span data-ttu-id="a926a-136">Następnie należy toocollect niektóre informacje na temat aplikacji hello, używanego podczas hello PingAccess czynności.</span><span class="sxs-lookup"><span data-stu-id="a926a-136">Then, you need toocollect some information about hello app that you can use during hello PingAccess steps.</span></span>

<span data-ttu-id="a926a-137">Wykonaj te kroki toopublish aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a926a-137">Follow these steps toopublish your app.</span></span> <span data-ttu-id="a926a-138">Bardziej szczegółowe wskazówki kroki 1 – 8, zobacz [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a926a-138">For a more detailed walkthrough of steps 1-8, see [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

1. <span data-ttu-id="a926a-139">Jeśli nie w ostatniej sekcji hello, zaloguj się w toohello [portalu Azure](https://portal.azure.com) jako administrator globalny.</span><span class="sxs-lookup"><span data-stu-id="a926a-139">If you didn't in hello last section, sign in toohello [Azure portal](https://portal.azure.com) as a global administrator.</span></span>
2. <span data-ttu-id="a926a-140">Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="a926a-140">Select **Azure Active Directory** > **Enterprise applications**.</span></span>
3. <span data-ttu-id="a926a-141">Wybierz **Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="a926a-141">Select **Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="a926a-142">Wybierz **lokalnej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a926a-142">Select **On-premises application**.</span></span>
5. <span data-ttu-id="a926a-143">Wypełnij pola hello wymagane informacje o nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a926a-143">Fill out hello required fields with information about your new app.</span></span> <span data-ttu-id="a926a-144">Użyj hello następujące wskazówki dotyczące ustawień hello:</span><span class="sxs-lookup"><span data-stu-id="a926a-144">Use hello following guidance for hello settings:</span></span>
   - <span data-ttu-id="a926a-145">**Wewnętrzny adres URL**: zwykle Podaj adres URL hello przejście toohello aplikacji zaloguj się na stronie podczas pracy w sieci firmowej hello.</span><span class="sxs-lookup"><span data-stu-id="a926a-145">**Internal URL**: Normally you provide hello URL that takes you toohello app’s sign in page when you’re on hello corporate network.</span></span> <span data-ttu-id="a926a-146">W tym scenariuszu hello łącznika musi tootreat hello PingAccess proxy jako pierwsza strona hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a926a-146">For this scenario hello connector needs tootreat hello PingAccess proxy as hello front page of hello app.</span></span> <span data-ttu-id="a926a-147">Użyj tego formatu: `https://<host name of your PA server>:<port>`.</span><span class="sxs-lookup"><span data-stu-id="a926a-147">Use this format: `https://<host name of your PA server>:<port>`.</span></span> <span data-ttu-id="a926a-148">Hello port jest 3000 domyślnie, ale można go skonfigurować w PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a926a-148">hello port is 3000 by default, but you can configure it in PingAccess.</span></span>
   - <span data-ttu-id="a926a-149">**Metoda wstępnego uwierzytelnienia**: Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a926a-149">**Pre-authentication method**: Azure Active Directory</span></span>
   - <span data-ttu-id="a926a-150">**Tłumaczenie adresów URL w nagłówkach**: nie</span><span class="sxs-lookup"><span data-stu-id="a926a-150">**Translate URL in Headers**: No</span></span>

   >[!NOTE]
   ><span data-ttu-id="a926a-151">Jeśli jest to swoją pierwszą aplikację, użyj port 3000 toostart i wróć tooupdate to ustawienie w przypadku zmiany konfiguracji PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a926a-151">If this is your first application, use port 3000 toostart and come back tooupdate this setting if you change your PingAccess configuration.</span></span> <span data-ttu-id="a926a-152">Jeśli jest to drugi lub nowszym aplikacji, to należy toomatch hello skonfigurowaniu PingAccess odbiornika.</span><span class="sxs-lookup"><span data-stu-id="a926a-152">If this is your second or later app, this will need toomatch hello Listener you’ve configured in PingAccess.</span></span> <span data-ttu-id="a926a-153">Dowiedz się więcej o [odbiorników w PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span><span class="sxs-lookup"><span data-stu-id="a926a-153">Learn more about [listeners in PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).</span></span>

6. <span data-ttu-id="a926a-154">Wybierz **Dodaj** u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="a926a-154">Select **Add** at hello bottom of hello blade.</span></span> <span data-ttu-id="a926a-155">Aplikacja zostanie dodany, a następnie otwiera hello szybki start menu.</span><span class="sxs-lookup"><span data-stu-id="a926a-155">Your application is added, and hello quick start menu opens.</span></span>
7. <span data-ttu-id="a926a-156">Witaj szybki start menu wybierz **przypisać użytkownika do testowania**i Dodaj przynajmniej jednego użytkownika toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a926a-156">In hello quick start menu, select **Assign a user for testing**, and add at least one user toohello application.</span></span> <span data-ttu-id="a926a-157">Upewnij się, że to konto testu ma dostęp toohello lokalnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a926a-157">Make sure this test account has access toohello on-premises application.</span></span>
8. <span data-ttu-id="a926a-158">Wybierz **przypisać** przypisanie użytkownika testu hello toosave.</span><span class="sxs-lookup"><span data-stu-id="a926a-158">Select **Assign** toosave hello test user assignment.</span></span>
9. <span data-ttu-id="a926a-159">W bloku zarządzania aplikacji hello, wybierz **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="a926a-159">On hello app management blade, select **Single sign-on**.</span></span>
10. <span data-ttu-id="a926a-160">Wybierz **na podstawie nagłówka logowania jednokrotnego** z menu rozwijanego hello.</span><span class="sxs-lookup"><span data-stu-id="a926a-160">Choose **Header-based sign-on** from hello drop-down menu.</span></span> <span data-ttu-id="a926a-161">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a926a-161">Select **Save**.</span></span>

   >[!TIP]
   ><span data-ttu-id="a926a-162">Jeśli jest to pierwsza przy użyciu opartych na nagłówkach logowanie jednokrotne, należy tooinstall PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a926a-162">If this is your first time using header-based single sign-on, you need tooinstall PingAccess.</span></span> <span data-ttu-id="a926a-163">toomake się, że subskrypcji platformy Azure jest automatycznie kojarzony z instalacją PingAccess, użyj łącza hello na tym toodownload strony rejestracji jednokrotnej PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a926a-163">toomake sure your Azure subscription is automatically associated with your PingAccess installation, use hello link on this single sign-on page toodownload PingAccess.</span></span> <span data-ttu-id="a926a-164">Można teraz otworzyć hello pobierania witryny lub powracanie toothis strony.</span><span class="sxs-lookup"><span data-stu-id="a926a-164">You can open hello download site now, or come back toothis page later.</span></span> 

   ![Wybierz na podstawie nagłówka logowania jednokrotnego](./media/application-proxy-ping-access/sso-header.PNG)

11. <span data-ttu-id="a926a-166">Zamknij blok aplikacje przedsiębiorstwa hello lub przewiń wszystkich hello sposób toohello tooreturn po lewej stronie toohello usługi Azure Active Directory menu.</span><span class="sxs-lookup"><span data-stu-id="a926a-166">Close hello Enterprise applications blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
12. <span data-ttu-id="a926a-167">Wybierz **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="a926a-167">Select **App registrations**.</span></span>

   ![Wybierz rejestracji aplikacji](./media/application-proxy-ping-access/app-registrations.png)

13. <span data-ttu-id="a926a-169">Aplikacja hello wybierz dodaną, następnie **adresy URL odpowiedzi**.</span><span class="sxs-lookup"><span data-stu-id="a926a-169">Select hello app you just added, then **Reply URLs**.</span></span>

   ![Wybierz adresy URL odpowiedzi](./media/application-proxy-ping-access/reply-urls.png)

14. <span data-ttu-id="a926a-171">Określ, czy toosee hello zewnętrznego adresu URL, zostanie przypisany tooyour aplikacja w kroku 5 się na liście adresów URL odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="a926a-171">Check toosee if hello external URL that you assigned tooyour app in step 5 is in hello Reply URLs list.</span></span> <span data-ttu-id="a926a-172">Jeśli nie, dodaj go.</span><span class="sxs-lookup"><span data-stu-id="a926a-172">If it’s not, add it now.</span></span>
15. <span data-ttu-id="a926a-173">W bloku ustawień aplikacji hello wybierz **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="a926a-173">On hello app settings blade, select **Required permissions**.</span></span>

  ![Wybierz wymagane uprawnienia](./media/application-proxy-ping-access/required-permissions.png)

16. <span data-ttu-id="a926a-175">Wybierz pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a926a-175">Select **Add**.</span></span> <span data-ttu-id="a926a-176">Hello interfejsu API, można wybrać **Windows Azure Active Directory**, następnie **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="a926a-176">For hello API, choose **Windows Azure Active Directory**, then **Select**.</span></span> <span data-ttu-id="a926a-177">Uprawnienia hello, wybierz **odczytu i zapisu wszystkie aplikacje** i **Zaloguj się i odczytuj profil użytkownika**, następnie **wybierz** i **gotowe**.</span><span class="sxs-lookup"><span data-stu-id="a926a-177">For hello permissions, choose **Read and write all applications** and **Sign in and read user profile**, then **Select** and **Done**.</span></span>  

  ![Wybierz uprawnienia](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a><span data-ttu-id="a926a-179">Zbieranie informacji o krokach PingAccess hello</span><span class="sxs-lookup"><span data-stu-id="a926a-179">Collect information for hello PingAccess steps</span></span>

1. <span data-ttu-id="a926a-180">W bloku ustawień aplikacji, wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="a926a-180">On your app settings blade, select **Properties**.</span></span> 

  ![Wybierz polecenie Właściwości](./media/application-proxy-ping-access/properties.png)

2. <span data-ttu-id="a926a-182">Zapisz hello **identyfikator aplikacji** wartość.</span><span class="sxs-lookup"><span data-stu-id="a926a-182">Save hello **Application Id** value.</span></span> <span data-ttu-id="a926a-183">Służy to dla Identyfikatora klienta powitania po skonfigurowaniu PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a926a-183">This is used for hello client ID when you configure PingAccess.</span></span>
3. <span data-ttu-id="a926a-184">W bloku ustawień aplikacji hello wybierz **klucze**.</span><span class="sxs-lookup"><span data-stu-id="a926a-184">On hello app settings blade, select **Keys**.</span></span>

  ![Wybierz klucze](./media/application-proxy-ping-access/Keys.png)

4. <span data-ttu-id="a926a-186">Utwórz klucz, wprowadzając opis klucza i wybierając z menu rozwijanego hello datę wygaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="a926a-186">Create a key by entering a key description and choosing an expiration date from hello drop-down menu.</span></span>
5. <span data-ttu-id="a926a-187">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a926a-187">Select **Save**.</span></span> <span data-ttu-id="a926a-188">Identyfikator GUID jest wyświetlana w hello **wartość** pola.</span><span class="sxs-lookup"><span data-stu-id="a926a-188">A GUID appears in hello **Value** field.</span></span>

  <span data-ttu-id="a926a-189">Zapisz tę wartość teraz, ponieważ nie będzie możliwe toosee ją ponownie po zamknąć to okno.</span><span class="sxs-lookup"><span data-stu-id="a926a-189">Save this value now, as you won’t be able toosee it again after you close this window.</span></span>

  ![Utwórz nowy klucz](./media/application-proxy-ping-access/create-keys.png)

6. <span data-ttu-id="a926a-191">Zamknij bloku rejestracji aplikacji hello lub przewiń wszystkich hello sposób toohello tooreturn po lewej stronie toohello usługi Azure Active Directory menu.</span><span class="sxs-lookup"><span data-stu-id="a926a-191">Close hello App registrations blade or scroll all hello way toohello left tooreturn toohello Azure Active Directory menu.</span></span>
7. <span data-ttu-id="a926a-192">Wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="a926a-192">Select **Properties**.</span></span>
8. <span data-ttu-id="a926a-193">Zapisz hello **identyfikator katalogu** identyfikatora GUID.</span><span class="sxs-lookup"><span data-stu-id="a926a-193">Save hello **Directory ID** GUID.</span></span>

### <a name="optional---update-graphapi-toosend-custom-fields"></a><span data-ttu-id="a926a-194">Opcjonalne - pola niestandardowe toosend GraphAPI aktualizacji</span><span class="sxs-lookup"><span data-stu-id="a926a-194">Optional - Update GraphAPI toosend custom fields</span></span>

<span data-ttu-id="a926a-195">Aby uzyskać listę tokeny zabezpieczające, które wysyła usługi Azure AD do uwierzytelniania, zobacz [odwołania do tokenu usługi Azure AD](./develop/active-directory-token-and-claims.md).</span><span class="sxs-lookup"><span data-stu-id="a926a-195">For a list of security tokens that Azure AD sends for authentication, see [Azure AD token reference](./develop/active-directory-token-and-claims.md).</span></span> <span data-ttu-id="a926a-196">Niestandardowe oświadczenie, które wysyła innych tokenów, należy użyć pola aplikacji hello tooset GraphAPI *acceptMappedClaims* za**True**.</span><span class="sxs-lookup"><span data-stu-id="a926a-196">If you need a custom claim that sends other tokens, use GraphAPI tooset hello app field *acceptMappedClaims* too**True**.</span></span> <span data-ttu-id="a926a-197">Azure AD Graph Explorer lub MS Graph toomake można użyć tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a926a-197">You can use either Azure AD Graph Explorer or MS Graph toomake this configuration.</span></span> 

<span data-ttu-id="a926a-198">W tym przykładzie użyto wykres Explorer:</span><span class="sxs-lookup"><span data-stu-id="a926a-198">This example uses Graph Explorer:</span></span>

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a><span data-ttu-id="a926a-199">Pobierz PingAccess i konfigurowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="a926a-199">Download PingAccess and configure your app</span></span>

<span data-ttu-id="a926a-200">Teraz, gdy zakończyła się wszystkie kroki konfiguracji usługi Azure Active Directory hello, można przenieść na tooconfiguring PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a926a-200">Now that you've completed all hello Azure Active Directory setup steps, you can move on tooconfiguring PingAccess.</span></span> 

<span data-ttu-id="a926a-201">Hello szczegółowe informacje na temat hello PingAccess częścią tego scenariusza kontynuowania hello dokumentacji tożsamości Ping [PingAccess konfigurowanie dla usługi Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span><span class="sxs-lookup"><span data-stu-id="a926a-201">hello detailed steps for hello PingAccess part of this scenario continue in hello Ping Identity documentation, [Configure PingAccess for Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).</span></span>

<span data-ttu-id="a926a-202">Tych krokach objaśniono proces hello pierwsze konto PingAccess, jeśli nie masz już konto, instalowanie hello PingAccess serwera i tworzenie połączenia dostawcy usługi Azure AD OIDC z hello identyfikator katalogu, który został skopiowany z portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a926a-202">Those steps walk you through hello process of getting a PingAccess account if you don't already have one, installing hello PingAccess Server, and creating an Azure AD OIDC Provider connection with hello Directory ID that you copied from hello Azure portal.</span></span> <span data-ttu-id="a926a-203">Następnie należy użyć hello aplikacji identyfikator i klucz wartości toocreate sesji sieci Web na PingAccess.</span><span class="sxs-lookup"><span data-stu-id="a926a-203">Then, you use hello Application ID and Key values toocreate a Web Session on PingAccess.</span></span> <span data-ttu-id="a926a-204">Po wykonaniu tej można Konfigurowanie mapowania tożsamości i tworzenia hostów wirtualnych, witryn i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a926a-204">After that, you can set up identity mapping and create a virtual host, site, and application.</span></span>

### <a name="test-your-app"></a><span data-ttu-id="a926a-205">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="a926a-205">Test your app</span></span>

<span data-ttu-id="a926a-206">Po zakończeniu wszystkich tych kroków aplikacji powinna być uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a926a-206">When you've completed all these steps, your app should be up and running.</span></span> <span data-ttu-id="a926a-207">tootest, otwórz przeglądarkę i przejdź toohello zewnętrzny adres URL, utworzony po opublikowaniu aplikacji hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a926a-207">tootest it, open a browser and navigate toohello external URL that you created when you published hello app in Azure.</span></span> <span data-ttu-id="a926a-208">Zaloguj się przy użyciu konta testowego hello tego przypisanej toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a926a-208">Sign in with hello test account that you assigned toohello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a926a-209">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a926a-209">Next steps</span></span>

- [<span data-ttu-id="a926a-210">Skonfiguruj PingAccess dla usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a926a-210">Configure PingAccess for Azure AD</span></span>](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [<span data-ttu-id="a926a-211">W jaki sposób serwera Proxy aplikacji usługi Azure AD zapewnia rejestrację jednokrotną</span><span class="sxs-lookup"><span data-stu-id="a926a-211">How does Azure AD Application Proxy provide single sign-on?</span></span>](application-proxy-sso-overview.md)
- [<span data-ttu-id="a926a-212">Rozwiązywanie problemów z serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="a926a-212">Troubleshoot Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)
