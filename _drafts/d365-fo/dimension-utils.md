# Introduction

The following snippet is used to retrieve individual dimension values from the DimensionAttributeValueCombination table.

```xpp
internal final class DimensionUtils
{
    public static DimensionValue getDimensionValue(DimensionAttributeValueCombination _davc, Name _dimensionName)
    {
        DimensionAttribute dimensionAttribute = DimensionAttribute::findByName(_dimensionName);

        if (!dimensionAttribute)
        {
            // The given dimension does not exist.
            throw error(Error::wrongUseOfFunction(funcName()));
        }

        FieldId fieldId = DimensionAttributeValueCombination::getDimensionValueFieldId(dimensionAttribute.Name);
        return _davc.(fieldId);
    }
}
```

The following snippet is used to get a default dimension with a modified dimension value.

```xpp
internal final class DimensionUtils
{
    public RecId replaceDefaultDimensionValue(DimensionValue _value, DimensionDefault _defaultDimension, Name _dimensionName)
    {
        DimensionAttributeValue             dimAttrValue;
        DimensionAttribute                  dimAttr;
        DimensionAttributeValueSetStorage   davss;
        RecId                               defaultDimension = _defaultDimension;

        if (!_value)
        {
            return defaultDimension;
        }

        dimAttr = DimensionAttribute::findByName(_dimensionName);

        if (!dimAttr)
        {
            throw error(strFmt("@AVAFaros:AVAImportPayrollService_NoFinancialDimensionNameError", _dimensionName));
        }

        dimAttrValue = DimensionAttributeValue::findByDimensionAttributeAndValue(dimAttr, _value, false, true);
    
        if (dimAttrValue)
        {
            davss = DimensionAttributeValueSetStorage::find(_defaultDimension);
            davss.addItem(dimAttrValue);
            defaultDimension = davss.save();
        }

        return defaultDimension;
    }  
}
```

The following snippet is used to merge 2 default dimension. If both default dimension contain a value for the same attribute the vale of the first default dimension will be taken.

```xpp
internal final class DimensionUtils
{
    public DimensionDefault mergeDimension(
        DimensionDefault _primaryDefaultDimension,
        DimensionDefault _secondaryDefaultDimension,
        DimensionDefaultMap _dimensionDefaultMap)
    {
        return DimensionMerge::newFromTable(
            _dimensionDefaultMap,
            CompanyInfo::current()
        ).merge(_primaryDefaultDimension, _secondaryDefaultDimension);   
    }
}
```

The following snippet is used to find or create a LedgerDiemnsion for a given MainAccount and DefaultDimension:

```xpp
internal final class DimensionUtils
{
    public LedgerDimensionAccount createLedgerDimensionFromMainAccountId(
        MainAccount                     _mainAccount,
        LedgerDefaultDimensionValueSet  _defaultDimensionRecId)
    {
        return LedgerDimensionFacade::serviceCreateLedgerDimension(
            LedgerDefaultAccountHelper::getDefaultAccountFromMainAccountRecId(_mainAccount.RecId), _defaultDimensionRecId
        );
    }
}
```
