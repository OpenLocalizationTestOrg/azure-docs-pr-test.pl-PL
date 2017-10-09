## <a name="create-a-ruby-application"></a><span data-ttu-id="415ea-101">Tworzenie aplikacji Ruby</span><span class="sxs-lookup"><span data-stu-id="415ea-101">Create a Ruby application</span></span>
<span data-ttu-id="415ea-102">Aby uzyskać instrukcje, zobacz [tworzenie aplikacji Ruby na platformie Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="415ea-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="415ea-103">Konfigurowanie sieci tooUse aplikacji usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="415ea-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="415ea-104">toouse usługi Service Bus pobranie i użycie hello Azure Ruby pakiet, który zawiera zestaw wygody bibliotek, które komunikują się z usługi REST magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="415ea-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="415ea-105">Użyj RubyGems tooobtain hello pakietu</span><span class="sxs-lookup"><span data-stu-id="415ea-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="415ea-106">Użyj interfejsu wiersza polecenia, takich jak **PowerShell** (system Windows), **terminali** (Mac), lub **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="415ea-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="415ea-107">Wpisz "gem zainstalować program azure" hello polecenia okna tooinstall hello gem i zależności.</span><span class="sxs-lookup"><span data-stu-id="415ea-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="415ea-108">Importowanie pakietu hello</span><span class="sxs-lookup"><span data-stu-id="415ea-108">Import hello package</span></span>
<span data-ttu-id="415ea-109">Za pomocą edytora tekstu, dodać powitania od góry toohello hello Ruby pliku, w którym planujesz toouse magazynu:</span><span class="sxs-lookup"><span data-stu-id="415ea-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="415ea-110">Skonfiguruj połączenie usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="415ea-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="415ea-111">Użyj hello poniższy kod tooset hello wartości przestrzeni nazw, nazwę hello klucza, klucz podpisujący i hosta:</span><span class="sxs-lookup"><span data-stu-id="415ea-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="415ea-112">Wartość hello przestrzeni nazw wartość toohello utworzonego zamiast hello cały adres URL.</span><span class="sxs-lookup"><span data-stu-id="415ea-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="415ea-113">Na przykład użyć **"yourexamplenamespace"**, nie "yourexamplenamespace.servicebus.windows.net".</span><span class="sxs-lookup"><span data-stu-id="415ea-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
