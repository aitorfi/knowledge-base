# Introduction

The following snippet is used to change an amount to another currency using a specific exchange rate type and a date.

```xpp
internal final class CustomCurrencyExchangeHelper
{
    public static Amount exchangeAmount(ExchangeRateTypeRecId _exchRateTypeRecId, Amount _fromAmount, CurrencyCode _fromCurrencyCode, CurrencyCode _toCurrencyCode, date _exchangeDate = systemDateGet())
    {
        try
        {
            CurrencyExchangeHelper currencyExchangeHelper = CurrencyExchangeHelper::newExchangeDate(Ledger::current(), _exchangeDate);
            currencyExchangeHelper.parmExchangeRateTypeRecId(_exchRateTypeRecId);
            return currencyExchangeHelper.calculateCurrencyToCurrency(
                _fromCurrencyCode,
                _toCurrencyCode,
                _fromAmount,
                true
            );
        }
        catch
        {
            // An exception will be thrown if an exchange rate cannot be found.
            return 0;
        }
    }
}
```
