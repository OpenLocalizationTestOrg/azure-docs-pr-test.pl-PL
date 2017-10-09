## <a name="create-a-ruby-application"></a>Tworzenie aplikacji Ruby
Aby uzyskać instrukcje, zobacz [tworzenie aplikacji Ruby na platformie Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-toouse-service-bus"></a>Konfigurowanie sieci tooUse aplikacji usługi Service Bus
toouse usługi Service Bus pobranie i użycie hello Azure Ruby pakiet, który zawiera zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Użyj RubyGems tooobtain hello pakietu
1. Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).
2. Wpisz "gem zainstalować program azure" hello polecenia okna tooinstall hello gem i zależności.

### <a name="import-hello-package"></a>Importowanie pakietu hello
Za pomocą edytora tekstu, dodać powitania od góry toohello hello Ruby pliku, w którym planujesz toouse magazynu:

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a>Skonfiguruj połączenie usługi Service Bus
Użyj hello poniższy kod tooset hello wartości przestrzeni nazw, nazwę hello klucza, klucz podpisujący i hosta:

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

Wartość hello przestrzeni nazw wartość toohello utworzonego zamiast hello cały adres URL. Na przykład użyć **"yourexamplenamespace"**, nie "yourexamplenamespace.servicebus.windows.net".
