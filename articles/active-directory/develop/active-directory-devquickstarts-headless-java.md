---
title: "aaaAzure wiersza polecenia języka AD Java wprowadzenie | Dokumentacja firmy Microsoft"
description: "Jak toobuild Java polecenia aplikacji wiersza, który podpisuje użytkowników w tooaccess interfejsu API."
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="15ba6-103">Przy użyciu tooAccess Java wiersza polecenia aplikacji interfejsu API w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="15ba6-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="15ba6-104">Usługi Azure AD, ułatwia toooutsource proste i bezpośrednie zarządzanie tożsamościami aplikacji sieci web, zapewniając pojedyncze logowania i wylogowywania przy tylko kilku wierszy kodu.</span><span class="sxs-lookup"><span data-stu-id="15ba6-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="15ba6-105">W aplikacjach sieci web Java można to zrobić za pomocą implementacji hello społeczność ADAL4J firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="15ba6-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="15ba6-106">W tym miejscu użyjemy ADAL4J do:</span><span class="sxs-lookup"><span data-stu-id="15ba6-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="15ba6-107">Użytkownik hello logowania do aplikacji hello przy użyciu usługi Azure AD jako dostawcy tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="15ba6-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="15ba6-108">Wyświetlane informacje o hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="15ba6-108">Display some information about hello user.</span></span>
* <span data-ttu-id="15ba6-109">Znak hello użytkownika poza aplikacją hello.</span><span class="sxs-lookup"><span data-stu-id="15ba6-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="15ba6-110">W kolejności toodo to, musisz:</span><span class="sxs-lookup"><span data-stu-id="15ba6-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="15ba6-111">Rejestrowanie aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="15ba6-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="15ba6-112">Konfigurowanie biblioteki ADAL4J hello toouse aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15ba6-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="15ba6-113">Użyj hello ADAL4J biblioteki tooissue logowania i wylogowywania żądań tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="15ba6-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="15ba6-114">Wydrukować dane dotyczące hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="15ba6-114">Print out data about hello user.</span></span>

<span data-ttu-id="15ba6-115">Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="15ba6-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="15ba6-116">Należy również dzierżawa usługi Azure AD, w których tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15ba6-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="15ba6-117">Jeśli nie masz już, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="15ba6-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="15ba6-118">1.  Rejestrowanie aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="15ba6-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="15ba6-119">tooenable tooauthenticate użytkowników aplikacji, musisz najpierw tooregister nową aplikację w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="15ba6-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="15ba6-120">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15ba6-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="15ba6-121">Na górnym pasku hello, kliknij na Twoim koncie, a w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, którym chcesz tooregister aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15ba6-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="15ba6-122">Polecenie **więcej usług** w hello nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="15ba6-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="15ba6-123">Polecenie **rejestracji aplikacji** i wybierz polecenie **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="15ba6-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="15ba6-124">Postępuj zgodnie z monitami hello i utworzyć nową **aplikacji sieci Web i/lub WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="15ba6-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="15ba6-125">Witaj **nazwa** z hello aplikacji opisano użytkownikom tooend aplikacji</span><span class="sxs-lookup"><span data-stu-id="15ba6-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="15ba6-126">Witaj **adres URL logowania** jest hello podstawowy adres URL aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15ba6-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="15ba6-127">Domyślnie Hello szkielet `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="15ba6-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="15ba6-128">Po zakończeniu rejestracji usługi AAD przypisze aplikacji Unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15ba6-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="15ba6-129">Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go na karcie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="15ba6-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="15ba6-130">Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15ba6-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="15ba6-131">Witaj **identyfikator URI aplikacji** to unikatowy identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="15ba6-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="15ba6-132">Konwencja Hello jest toouse `https://<tenant-domain>/<app-name>`, np. `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="15ba6-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="15ba6-133">Raz w portalu hello aplikacji należy utworzyć **klucza** z hello **ustawienia** strony dla aplikacji i skopiuj go.</span><span class="sxs-lookup"><span data-stu-id="15ba6-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="15ba6-134">Będziesz potrzebować go za chwilę.</span><span class="sxs-lookup"><span data-stu-id="15ba6-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="15ba6-135">2. Konfigurowanie biblioteki ADAL4J toouse aplikacji, a za pomocą programu Maven wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="15ba6-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="15ba6-136">W tym miejscu skonfigurujemy ADAL4J toouse hello protokołu uwierzytelniania OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="15ba6-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="15ba6-137">ADAL4J być używane tooissue żądań logowania i wylogowywania, zarządzanie sesji użytkownika hello i uzyskać informacje o użytkowniku hello, między innymi.</span><span class="sxs-lookup"><span data-stu-id="15ba6-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="15ba6-138">W katalogu głównym projektu hello, otworzyć/utworzyć `pom.xml` i Znajdź hello `// TODO: provide dependencies for Maven` i Zastąp hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="15ba6-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="15ba6-139">3. Utwórz plik Java PublicClient hello</span><span class="sxs-lookup"><span data-stu-id="15ba6-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="15ba6-140">Jak wspomniano powyżej, użyjemy hello interfejsu API programu Graph tooget dane dotyczące hello zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="15ba6-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="15ba6-141">Ta ułatwia nam toobe możemy utworzyć toorepresent pliku **obiektu katalogu** i hello toorepresent pojedynczego pliku **użytkownika** tak, aby hello wzorzec OO programu Java może służyć.</span><span class="sxs-lookup"><span data-stu-id="15ba6-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="15ba6-142">Utwórz plik o nazwie `DirectoryObject.java` użyjemy toostore podstawowe dane o wszelkich DirectoryObject (można uważasz, że wolne toouse to później dla innych zapytań wykresu, możesz to zrobić).</span><span class="sxs-lookup"><span data-stu-id="15ba6-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="15ba6-143">Użytkownik może wycinania/wklejania to poniżej:</span><span class="sxs-lookup"><span data-stu-id="15ba6-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="15ba6-144">Kompilowanie i uruchamianie przykładowych hello</span><span class="sxs-lookup"><span data-stu-id="15ba6-144">Compile and run hello sample</span></span>
<span data-ttu-id="15ba6-145">Zmień wstecz out tooyour główny katalog i uruchom hello następujące przykładowe hello toobuild polecenia możesz umieścić tylko ze sobą przy użyciu `maven`.</span><span class="sxs-lookup"><span data-stu-id="15ba6-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="15ba6-146">Zostaną użyte hello `pom.xml` pliku zapisano zależności.</span><span class="sxs-lookup"><span data-stu-id="15ba6-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="15ba6-147">Po wykonaniu `adal4jsample.war` plików w sieci `/targets` katalogu.</span><span class="sxs-lookup"><span data-stu-id="15ba6-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="15ba6-148">Może wdrożyć który w Twojej kontenera Tomcat i odwiedź adres URL hello</span><span class="sxs-lookup"><span data-stu-id="15ba6-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="15ba6-149">Jest bardzo proste toodeploy WAR z hello najnowsze serwery Tomcat.</span><span class="sxs-lookup"><span data-stu-id="15ba6-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="15ba6-150">Po prostu przejdź zbyt`http://localhost:8080/manager/` i wykonać instrukcje hello przekazywania Twojej '' adal4jsample.war "pliku.</span><span class="sxs-lookup"><span data-stu-id="15ba6-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="15ba6-151">Autodeploy go zostanie automatycznie z hello właściwego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="15ba6-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="15ba6-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="15ba6-152">Next Steps</span></span>
<span data-ttu-id="15ba6-153">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="15ba6-153">Congratulations!</span></span> <span data-ttu-id="15ba6-154">Teraz masz pracy aplikacji Java, która ma hello możliwości tooauthenticate użytkowników, bezpiecznie wywoływać interfejsy API sieci Web przy użyciu protokołu OAuth 2.0, a uzyskać podstawowe informacje o użytkowniku hello.</span><span class="sxs-lookup"><span data-stu-id="15ba6-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="15ba6-155">Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="15ba6-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="15ba6-156">Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), lub można ją sklonować z serwisu GitHub:</span><span class="sxs-lookup"><span data-stu-id="15ba6-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

