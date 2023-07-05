**Google Sheets currency converter**

While working on a project for my master's program, I needed to convert and unify multiple different currencies into a single currency, USD. However, I couldn’t find an easy way to accomplish this.

I had historical price data for several companies, but since these companies were based in different countries, the data was in various currencies.

This script helped me. 

*   In Google Sheets, click on Extensions, and then on Apps Script.
*   Paste the following code

```javascript
function HISTORICAL_EXCHANGE_RATE(date, fromCurrency, toCurrency) {
 var url = "https://api.exchangerate.host/convert";
 var queryUrl = url + "?from=" + fromCurrency + "&to=" + toCurrency + "&date=" + Utilities.formatDate(new Date(date), "GMT", "yyyy-MM-dd");
 var response = UrlFetchApp.fetch(queryUrl);
 var jsonResponse = JSON.parse(response.getContentText());
 return jsonResponse.info.rate;
}
```

*   Save the script
*   Go back to your Google sheet where you have dates and prices

Assuming you have dates in Column A and prices for Serbian Dinars in Column B, in Column C, use the following formula in the first row where you want to see the converted price:

\=A1 \* HISTORICAL\_EXCHANGE\_RATE(A1, "RSD", "USD")

Column A should be _date_ in format YYYY-MM-DD and column B should be the amount that needs to be converted from one currency to another.

Historical rates are available for most currencies all the way back to the year of 1999.

List of supported currencies: https://api.exchangerate.host/symbols

Disclaimer:

This script utilizes the [exchangerate.host](https://exchangerate.host) API for currency exchange rate information. Big thanks to ExchangeRate team for providing this valuable service and making this service available to the public. If you find this service beneficial and wish to support its continued development and maintenance, consider making a donation to the ExchangeRate team ([https://exchangerate.host/#/donate](https://exchangerate.host/#/donate)).
