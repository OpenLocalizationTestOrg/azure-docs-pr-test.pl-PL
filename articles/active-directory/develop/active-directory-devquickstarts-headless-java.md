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
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a>Przy użyciu tooAccess Java wiersza polecenia aplikacji interfejsu API w usłudze Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Usługi Azure AD, ułatwia toooutsource proste i bezpośrednie zarządzanie tożsamościami aplikacji sieci web, zapewniając pojedyncze logowania i wylogowywania przy tylko kilku wierszy kodu.  W aplikacjach sieci web Java można to zrobić za pomocą implementacji hello społeczność ADAL4J firmy Microsoft.

  W tym miejscu użyjemy ADAL4J do:

* Użytkownik hello logowania do aplikacji hello przy użyciu usługi Azure AD jako dostawcy tożsamości hello.
* Wyświetlane informacje o hello użytkownika.
* Znak hello użytkownika poza aplikacją hello.

W kolejności toodo to, musisz:

1. Rejestrowanie aplikacji w usłudze Azure AD
2. Konfigurowanie biblioteki ADAL4J hello toouse aplikacji.
3. Użyj hello ADAL4J biblioteki tooissue logowania i wylogowywania żądań tooAzure AD.
4. Wydrukować dane dotyczące hello użytkownika.

Rozpoczęto, tooget [pobrać szkielet aplikacji hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) lub [pobieranie próbki ukończyć powitalnych](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).  Należy również dzierżawa usługi Azure AD, w których tooregister aplikacji.  Jeśli nie masz już, [Dowiedz się, jak tooget jedną](active-directory-howto-tenant.md).

## <a name="1--register-an-application-with-azure-ad"></a>1.  Rejestrowanie aplikacji w usłudze Azure AD
tooenable tooauthenticate użytkowników aplikacji, musisz najpierw tooregister nową aplikację w dzierżawie.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Na górnym pasku hello, kliknij na Twoim koncie, a w obszarze hello **katalogu** wybierz hello dzierżawy usługi Active Directory, którym chcesz tooregister aplikacji.
3. Polecenie **więcej usług** w hello nawigacji po lewej stronie i wybierz polecenie **usługi Azure Active Directory**.
4. Polecenie **rejestracji aplikacji** i wybierz polecenie **Dodaj**.
5. Postępuj zgodnie z monitami hello i utworzyć nową **aplikacji sieci Web i/lub WebAPI**.
  * Witaj **nazwa** z hello aplikacji opisano użytkownikom tooend aplikacji
  * Witaj **adres URL logowania** jest hello podstawowy adres URL aplikacji.  Domyślnie Hello szkielet `http://localhost:8080/adal4jsample/`.
6. Po zakończeniu rejestracji usługi AAD przypisze aplikacji Unikatowy identyfikator aplikacji.  Ta wartość jest potrzebny w kolejnych sekcjach hello, dlatego skopiuj go na karcie aplikacji hello.
7. Z hello **ustawienia** -> **właściwości** strony dla aplikacji, aktualizacji hello identyfikator URI aplikacji. Witaj **identyfikator URI aplikacji** to unikatowy identyfikator aplikacji.  Konwencja Hello jest toouse `https://<tenant-domain>/<app-name>`, np. `http://localhost:8080/adal4jsample/`.

Raz w portalu hello aplikacji należy utworzyć **klucza** z hello **ustawienia** strony dla aplikacji i skopiuj go.  Będziesz potrzebować go za chwilę.

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a>2. Konfigurowanie biblioteki ADAL4J toouse aplikacji, a za pomocą programu Maven wymagania wstępne
W tym miejscu skonfigurujemy ADAL4J toouse hello protokołu uwierzytelniania OpenID Connect.  ADAL4J być używane tooissue żądań logowania i wylogowywania, zarządzanie sesji użytkownika hello i uzyskać informacje o użytkowniku hello, między innymi.

* W katalogu głównym projektu hello, otworzyć/utworzyć `pom.xml` i Znajdź hello `// TODO: provide dependencies for Maven` i Zastąp hello poniżej:

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



## <a name="3-create-hello-java-publicclient-file"></a>3. Utwórz plik Java PublicClient hello
Jak wspomniano powyżej, użyjemy hello interfejsu API programu Graph tooget dane dotyczące hello zalogowanego użytkownika. Ta ułatwia nam toobe możemy utworzyć toorepresent pliku **obiektu katalogu** i hello toorepresent pojedynczego pliku **użytkownika** tak, aby hello wzorzec OO programu Java może służyć.

* Utwórz plik o nazwie `DirectoryObject.java` użyjemy toostore podstawowe dane o wszelkich DirectoryObject (można uważasz, że wolne toouse to później dla innych zapytań wykresu, możesz to zrobić). Użytkownik może wycinania/wklejania to poniżej:

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


## <a name="compile-and-run-hello-sample"></a>Kompilowanie i uruchamianie przykładowych hello
Zmień wstecz out tooyour główny katalog i uruchom hello następujące przykładowe hello toobuild polecenia możesz umieścić tylko ze sobą przy użyciu `maven`. Zostaną użyte hello `pom.xml` pliku zapisano zależności.

`$ mvn package`

Po wykonaniu `adal4jsample.war` plików w sieci `/targets` katalogu. Może wdrożyć który w Twojej kontenera Tomcat i odwiedź adres URL hello 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> Jest bardzo proste toodeploy WAR z hello najnowsze serwery Tomcat. Po prostu przejdź zbyt`http://localhost:8080/manager/` i wykonać instrukcje hello przekazywania Twojej '' adal4jsample.war "pliku. Autodeploy go zostanie automatycznie z hello właściwego punktu końcowego.
> 
> 

## <a name="next-steps"></a>Następne kroki
Gratulacje! Teraz masz pracy aplikacji Java, która ma hello możliwości tooauthenticate użytkowników, bezpiecznie wywoływać interfejsy API sieci Web przy użyciu protokołu OAuth 2.0, a uzyskać podstawowe informacje o użytkowniku hello.  Jeśli nie jest jeszcze teraz jest hello toopopulate czas dzierżawy z niektórych użytkowników.

Odwołania, hello ukończone próbka (bez wartości konfiguracji) [jest dostarczane jako zip w tym miejscu](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), lub można ją sklonować z serwisu GitHub:

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

