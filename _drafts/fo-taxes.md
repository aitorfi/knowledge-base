The following snippet is used to calculate the tax base of an amount that includes taxes.

```
if (vendInvoiceInfoTable.InclTax)
{
    Amount amountExclTax = Tax::baseAmountExclTax(
        vendInvoiceInfoLine.TaxGroup,
        vendInvoiceInfoLine.TaxItemGroup,
        vendInvoiceInfoTable.TransDate,
        vendInvoiceInfoLine.CurrencyCode,
        vendInvoiceInfoLine.LineAmount,
        TaxModuleType::PurchInvoice
    );
}
```
