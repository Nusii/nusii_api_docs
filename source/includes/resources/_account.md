# Account

## Get my Account

```shell--curl
curl -X GET \
  -H 'User-Agent: Your App Name (www.yourapp.com)' \
  -H 'Content-Type: application/json' \
  -H "Authorization: Token token=YOUR_API_KEY" \
  "https://app.nusii.com/api/v2/account/me"
```

```shell--cli
nusii account
```

```ruby
require 'nusii-ruby'

Nusii.api_key = 'YOUR_API_KEY'
Nusii.user_agent = 'Your App Name (www.yourapp.com)'

Nusii::Account.me
```

```php
use Nusii\Nusii;

$nusii = new Nusii('YOUR_API_KEY');

$nusii->accounts()->me();
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "3",
    "type": "accounts",
    "attributes": {
      "email": "hello@your_company.com",
      "name": "Your Company Name",
      "subdomain": "your_company",
      "web": "www.your_company.com",
      "currency": "USD",
      "pdf_page_size": "A4",
      "locale": "en",
      "address": "Your Street Address 50",
      "address_state": "New York",
      "postcode": "10022",
      "city": "New York",
      "telephone": "1234567890",
      "default_theme": "clean"
    }
  }
}
```

This endpoint retrieves your personal account data.

### HTTP Request

`GET https://app.nusii.com/api/v2/account/me`
